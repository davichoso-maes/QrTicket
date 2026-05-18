# ADR-0007 — Usar funciones Lambda/serverless para operaciones de alta concurrencia

## Metadatos

| Campo | Valor |
|-------|-------|
| Número | `0007` |
| Título | Usar funciones Lambda/serverless para operaciones de alta concurrencia |
| Fecha | `17/05/2026` |
| Autor(es) | @davichoso |
| Estado | **Aceptada** |
| Alcance | Módulos de validación de tickets, webhooks de pago y reconciliación |
| Stakeholders consultados | Backend, DevOps, Producto |

## 1. Contexto

QrTicket enfrenta picos de carga extremos durante la apertura de puertas en eventos masivos: miles de validaciones de QR por minuto, webhooks de confirmación de pago y procesos de reconciliación nocturna. El monolito modular (ADR-0001) corre bien en carga normal, pero esos picos pueden saturar los pods y provocar colapso del sistema en el momento más crítico del negocio.

La arquitectura actual escala verticalmente y con réplicas horizontales fijas, lo que resulta costoso mantener en standby para picos que duran minutos u horas, y lento para escalar ante demanda repentina.

## 2. Alternativas consideradas

| Alternativa | Pros | Contras | Costo aproximado |
|-------------|------|---------|------------------|
| Escalar réplicas del monolito (horizontal) | sin cambios arquitecturales | costoso en standby; lento al escalar | alto (instancias siempre activas) |
| Queue + workers dedicados (RabbitMQ/BullMQ) | desacoplamiento de carga | infraestructura adicional a mantener | medio |
| Funciones Lambda/serverless (AWS Lambda / Vercel Functions) | escala a cero; pago por invocación; escala en segundos | cold start; límite de timeout; stateless | bajo (pay-per-use) |
| Edge functions (Cloudflare Workers) | latencia mínima; escala global | limitaciones de runtime (sin Node completo) | bajo |

## 3. Decisión

> Adoptar funciones Lambda/serverless para los tres casos de uso de alta concurrencia: **validación de QR en entrada a eventos**, **recepción y procesamiento de webhooks de pago** y **reconciliación nocturna de órdenes**. Se usará AWS Lambda (o Vercel Edge Functions para validaciones livianas) con una cola SQS/BullMQ como buffer para garantizar que ningún evento se pierda bajo carga extrema.

## 4. Consecuencias

### 4.1 Positivas

- El sistema principal no se satura durante picos de eventos masivos.
- Escala automáticamente de 0 a miles de invocaciones concurrentes en segundos.
- Costo proporcional al uso real; sin instancias en standby.
- Aísla fallos: un crash en validación no afecta el módulo de pagos ni la UI.

### 4.2 Negativas

- Cold start de ~200–500 ms en la primera invocación (mitigable con provisioned concurrency).
- Las funciones deben ser 100 % stateless; estado compartido sólo vía DB o caché externo.
- Mayor complejidad de observabilidad: logs dispersos entre Lambda, SQS y el monolito.
- Timeout máximo de 15 min en Lambda (suficiente para reconciliación, pero hay que diseñar para ello).

### 4.3 Neutras

- Requiere IaC (Terraform/SST) para gestionar funciones; alineado con el stack ya definido.
- El equipo debe familiarizarse con el modelo de ejecución serverless, aunque la curva es baja con Next.js API Routes como referencia.

## 5. Impacto en el sistema

| Módulo afectado | Cambio |
|-----------------|--------|
| `modules/access` | Endpoint de validación QR migra a Lambda; el monolito queda como orquestador |
| `modules/payments` | Webhook handler se extrae a función independiente con cola SQS |
| `modules/reports` | Job de reconciliación nocturna se convierte en Lambda programada (EventBridge) |
| AGENTS.md | Agregar agente `serverless-deployer` para gestión del ciclo de vida de funciones |
| CI/CD | Pipeline añade step de deploy serverless post-build |

## 6. Plan de reversión

Si las funciones Lambda presentan problemas de latencia inaceptables o errores persistentes en producción:

1. Reactivar los endpoints síncronos del monolito (ya existen, sólo están detrás de un feature flag).
2. Desactivar el enrutamiento hacia Lambda en el API Gateway.
3. Escalar réplicas del monolito temporalmente mientras se diagnostica.

El rollback no requiere cambios de código; sólo configuración de feature flags y variables de entorno.

## 7. Validación

- [ ] Load test con k6: simular 5.000 validaciones/min durante 10 min sin degradación.
- [ ] Cold start medido < 500 ms con warm-up configurado.
- [ ] Zero message loss en cola SQS bajo caída simulada de función (DLQ activo).
- [ ] Reconciliación nocturna completa en < 5 min para 10.000 órdenes.
- [ ] Alertas en CloudWatch/Datadog para error rate > 1 % y p99 > 2 s.

## 8. Referencias

- ADR-0001: Monolito modular con Next.js
- ADR-0003: Estrategia de colas y procesamiento asíncrono (si existe)
- [AWS Lambda best practices](https://docs.aws.amazon.com/lambda/latest/dg/best-practices.html)
- [Serverless Framework docs](https://www.serverless.com/framework/docs)

## 9. Historial

| Versión | Fecha | Autor | Cambio |
|---------|-------|-------|--------|
| v0.1 | 17/05/2026 | @davichoso | Decisión inicial — adoptar Lambda para alta concurrencia |
