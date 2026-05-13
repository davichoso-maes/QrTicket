# Business Requirements Document — QrTicket

> Documento de requisitos de negocio para QrTicket, alineado a [templates/BRD_TEMPLATE.md](../../templates/BRD_TEMPLATE.md) y aterrizado al contexto boliviano descrito en `CLAUDE.md`.

## 0. Metadatos

| Campo | Valor |
|-------|-------|
| Producto | Qrticket |
| Release evaluable | `release/1.0.0` |
| Sesión asociada | `S6` |
| Fecha de cierre | `13/05/2026` |
| Integrantes | `Antonio Ovando, @carlicode, Carla Marcela Florida Roman` |
| Versión | `v0.1` |
| Fecha | `13/05/2026` |
| Sponsor de negocio | Equipo fundador QrTicket |
| Stakeholders | Organizadores, universidades, asistentes, guardias, recintos, bancos, pasarelas QR, soporte operativo |
| Autores | Antonio Ovando, Carla Marcela Florida Roman |
| Revisores | Docente + 1 grupo par |
| Estado | Borrador |

## 1. Resumen ejecutivo

QrTicket nace para resolver un problema operativo muy concreto del mercado boliviano: la gestión de eventos sigue dependiendo de formularios, transferencias validadas manualmente, listas impresas, tickets falsificables y controles de acceso lentos. Esto castiga a tres actores a la vez: el organizador pierde tiempo y dinero, el asistente sufre fricción en compra e ingreso, y el guardia trabaja bajo presión sin herramientas confiables cuando falla la conectividad.

La propuesta es una plataforma SaaS de ticketing y control de acceso compuesta por dashboard web, app móvil de guardias con operación offline, tickets QR inteligentes, pagos por QR bancario y automatización conversacional por WhatsApp. El foco inicial es el ecosistema universitario boliviano, donde el dolor operativo es alto y la necesidad de profesionalización es evidente.

El valor esperado del MVP es medible: reducir el tiempo promedio de validación por asistente de 20-45 segundos a menos de 3 segundos, disminuir el fraude por tickets duplicados o falsificados a menos del 1%, reducir en al menos 70% el trabajo manual de conciliación y lograr que más del 60% de las compras se completen por canales digitales. Los KPIs principales son tiempo de validación, tasa de fraude, conversión de compra e ingresos procesados por evento.

Para avanzar se requiere aprobar el alcance del release 1.0.0, priorizar las integraciones de pago QR boliviano y habilitar la arquitectura offline-first para el flujo de guardias.

## 2. Contexto del negocio

- **Organización**: QrTicket, startup SaaS orientada a eventos universitarios y masivos.
- **Unidad impactada**: operación de eventos, venta de entradas, control de acceso y reporting post-evento.
- **Procesos de negocio afectados**: creación y publicación de eventos, venta y emisión de tickets, validación de pagos, control de accesos, conciliación financiera, analítica y auditoría.
- **Estrategia**: comenzar por el segmento universitario boliviano, donde la digitalización es baja pero la frecuencia de eventos y la adopción de WhatsApp/pagos QR hacen viable una rápida entrada al mercado.

## 3. Problema y oportunidad de negocio

### 3.1 Problema

En el contexto boliviano, la organización de eventos suele apoyarse en herramientas fragmentadas: formularios sueltos, hojas de cálculo, mensajería manual y comprobantes de pago verificados de forma artesanal. Esto produce al menos cuatro efectos negativos recurrentes. Primero, los asistentes enfrentan procesos burocráticos, filas y desconfianza al pagar. Segundo, los organizadores invierten demasiadas horas en registrar ventas, verificar depósitos, emitir listas y coordinar accesos. Tercero, los guardias operan con información incompleta y con riesgo alto de aceptar tickets duplicados. Cuarto, la dirección del evento termina sin métricas confiables para medir conversión, asistencia real y performance operativa.

Como hipótesis base de negocio para este release, el equipo asume que un evento universitario mediano de 300 a 800 asistentes pierde entre 8 y 20 horas hombre en conciliación manual, puede sufrir entre 3% y 10% de incidencias por tickets reenviados o duplicados, y vive saturación de ingresos cuando la red móvil falla. Si no se actúa, el organizador seguirá operando con costos ocultos, reputación afectada y capacidad de escalamiento limitada.

### 3.2 Oportunidad

- **Valor económico**: cobrar comisión por ticket, suscripción premium por organizador y servicios de setup para eventos grandes.
- **Valor operativo**: reducir filas, fraude, carga administrativa y tiempo de respuesta en puerta.
- **Valor estratégico**: ser una plataforma adaptada a Bolivia antes que un competidor internacional generalista.
- **Ventana de oportunidad**: alta adopción de WhatsApp, crecimiento del pago QR y ausencia de soluciones locales fuertes con modo offline para guardias.

### 3.3 Evidencia de discovery utilizada en esta versión

- **Fuente principal**: `CLAUDE.md` del proyecto como documento de visión y contexto del dominio.
- **Supuesto fuerte**: el segmento universitario es el mejor punto de entrada por frecuencia de eventos, urgencia operativa y baja profesionalización actual.
- **Cadencia deseada**: entrevistas semanales a organizadores, asistentes y guardias desde la siguiente iteración.

## 4. Usuarios objetivo / Personas clave

### 4.1 Persona principal — Organizador universitario

| Atributo | Valor |
|----------|-------|
| Nombre / rol | Carlos, presidente de centro de estudiantes |
| Contexto | Organiza congresos, seminarios, fiestas y actividades de recaudación con 200 a 1000 asistentes |
| Jobs-to-be-done | Crear el evento; publicar landing; vender tickets sin filas; confirmar pagos; coordinar guardias; ver métricas en tiempo real |
| Dolores principales | Usa Excel y WhatsApp para todo; pierde tiempo conciliando pagos; tiene miedo a tickets falsificados; no sabe cuánta gente realmente asistió |
| Ganancia esperada | Operar el evento desde un panel único, vender más rápido y tener control real de accesos e ingresos |

### 4.2 Persona secundaria — Asistente / comprador

| Atributo | Valor |
|----------|-------|
| Nombre / rol | María, estudiante universitaria |
| Contexto | Compra entradas desde el celular, usa WhatsApp a diario y está acostumbrada a pagar con QR bancario |
| Jobs-to-be-done | Encontrar el evento; comprar rápido; pagar sin efectivo; recibir ticket seguro; ingresar sin filas |
| Dolores principales | Formularios confusos, demora en confirmación, tickets que se pierden o no llegan, colas en el ingreso |
| Ganancia esperada | Comprar en minutos, recibir ticket digital y entrar sin fricción |

### 4.3 Persona terciaria — Guardia de acceso

| Atributo | Valor |
|----------|-------|
| Nombre / rol | Diego, guardia operativo |
| Contexto | Trabaja en puerta con presión alta, posibles problemas de red y necesidad de validar rápido |
| Jobs-to-be-done | Descargar evento; escanear QR; saber si el ticket es válido; seguir operando sin internet; sincronizar después |
| Dolores principales | Listas desactualizadas, mala señal, riesgo de doble acceso, poca visibilidad sobre incidentes |
| Ganancia esperada | Escaneo inmediato, feedback claro y sincronización confiable |

## 5. Propuesta de valor

| Eje | Contenido |
|-----|-----------|
| **Para quién** | Organizadores de eventos universitarios y masivos en Bolivia |
| **Qué necesita** | Gestionar eventos, vender tickets y controlar accesos con menor fricción y menor fraude |
| **Nuestra propuesta es** | Una plataforma modular con dashboard, venta multicanal, pagos QR, tickets digitales QR y validación online/offline |
| **Qué le aporta** | Menos trabajo manual, menos fraude, ingresos conciliados, acceso más rápido, trazabilidad operativa y métricas en tiempo real |
| **A diferencia de** | Formularios + Excel + WhatsApp manual o plataformas extranjeras no adaptadas al mercado local |
| **Nuestro diferencial es** | Adaptación a Bolivia, pagos QR bancarios, canal WhatsApp y operación offline para guardias |

## 6. Panorama competitivo (resumen)

| Competidor / alternativa | Tipo | Fortaleza percibida | Debilidad percibida |
|--------------------------|------|---------------------|---------------------|
| Excel + tickets impresos + transferencias | do-nothing | costo inicial bajo | alto fraude, cero trazabilidad, poca escalabilidad |
| Eventbrite | directo | producto maduro, marca conocida | menor adaptación a pagos QR Bolivia y operación offline |
| Passline | directo | experiencia de ticketing regional | menos enfoque en WhatsApp y contexto universitario boliviano |
| Todotix / boleterías locales | indirecto | conocimiento del mercado presencial | digitalización parcial, poca automatización operacional |
| Google Forms + WhatsApp | indirecto | simple de arrancar | sin antifraude, sin app de guardias, sin reporting serio |

## 7. Business Model Canvas

| Bloque | Elementos concretos |
|--------|----------------------|
| 1. Segmentos de clientes | universidades; centros de estudiantes; sociedades científicas; productoras; recintos; organizadores corporativos |
| 2. Propuesta de valor | tickets QR seguros; acceso offline; pagos QR locales; compra por WhatsApp; dashboard operativo |
| 3. Canales | web pública; dashboard SaaS; app guardias; app asistentes; WhatsApp bot |
| 4. Relación con clientes | autoservicio; onboarding guiado; soporte operativo por evento; mesa de ayuda por WhatsApp |
| 5. Fuentes de ingresos | comisión por ticket; plan mensual premium; setup fee para eventos masivos; personalización de branding |
| 6. Recursos clave | software; integraciones bancarias; infraestructura cloud; datos de eventos; equipo de producto e ingeniería |
| 7. Actividades clave | desarrollo; soporte; integración de pagos; operación de eventos; analítica; seguridad antifraude |
| 8. Socios clave | bancos; Libélula; Tigo Money; universidades; Meta WhatsApp API; recintos |
| 9. Estructura de costos | cloud; desarrollo; mensajería; soporte; adquisición de clientes; observabilidad |

## 8. Métricas clave de éxito

| ID | KPI | North Star? | Línea base | Meta | Horizonte | Fuente del dato |
|----|-----|-------------|------------|------|-----------|-----------------|
| KPI-01 | Tiempo mediano de validación de acceso | sí | 20-45 s manual | `<= 3 s` | release 1.0.0 + 90 días | `access_logs` |
| KPI-02 | Tasa de tickets fraudulentos o duplicados | no | 3-10% estimado | `< 1%` | 6 meses | `tickets` + incidencias |
| KPI-03 | Conversión visita a compra | no | sin medición | `>= 12%` | 6 meses | analytics + `orders/payments` |
| KPI-04 | Porcentaje de pagos conciliados automáticamente | no | ~0% manual | `>= 85%` | 6 meses | `payments` |
| KPI-05 | Porcentaje de validaciones resueltas offline y reconciliadas | no | 0% | `100% de tickets descargados` y `>= 95% sync posterior` | 6 meses | sync logs |
| KPI-06 | Eventos activos mensuales | no | 0 | `>= 20` | 12 meses | `events` |

## 9. Objetivos de negocio (SMART)

| ID | Objetivo | Métrica | Línea base | Meta | Horizonte |
|----|----------|---------|------------|------|-----------|
| BO-01 | Reducir el tiempo de validación por asistente | KPI-01 | 20-45 s | `<= 3 s` | Q4 2026 |
| BO-02 | Reducir el fraude por tickets | KPI-02 | 3-10% | `< 1%` | Q4 2026 |
| BO-03 | Aumentar la conversión digital de compra | KPI-03 | n/d | `>= 12%` | Q4 2026 |
| BO-04 | Automatizar la conciliación de pagos | KPI-04 | ~0% | `>= 85%` | Q4 2026 |
| BO-05 | Permitir continuidad operativa sin internet para guardias | KPI-05 | 0% | `100% cobertura offline descargada` | Q4 2026 |
| BO-06 | Alcanzar tracción inicial en el mercado universitario | KPI-06 | 0 | `>= 20 eventos/mes` | Q2 2027 |

## 10. Stakeholders y roles (RACI)

| Stakeholder | Interés | R / A / C / I |
|-------------|---------|----------------|
| Equipo fundador QrTicket | estrategia y negocio | A |
| Product / desarrollo | diseño e implementación | R |
| Organizadores | operación y feedback de producto | C |
| Guardias | operación en acceso | C |
| Asistentes | experiencia de compra e ingreso | I |
| Bancos y pasarelas | viabilidad de cobro | C |
| Universidades | validación institucional y adopción | C |
| Soporte operativo | continuidad del servicio | R |

## 11. Requerimientos de negocio

| ID | Requerimiento de negocio | Prioridad | Justificación | Métrica de aceptación |
|----|---------------------------|-----------|---------------|-----------------------|
| BR-001 | Permitir crear y administrar eventos desde un dashboard central | Must | es el núcleo del negocio | 100% de eventos gestionados desde la plataforma |
| BR-002 | Permitir vender entradas por al menos web y WhatsApp | Must | elimina barreras de compra | 2 canales activos en release 1.0.0 |
| BR-003 | Emitir tickets digitales con QR único por orden confirmada | Must | evita fraude y habilita validación | 100% de tickets con identificador único |
| BR-004 | Validar tickets en tiempo real con respuesta clara para el guardia | Must | control de acceso confiable | validación `<= 3 s` |
| BR-005 | Operar offline en la app de guardias | Must | continuidad operativa en eventos | dataset descargable y validación local |
| BR-006 | Integrar pagos QR bancarios adaptados a Bolivia | Must | adopción local | al menos 1 flujo QR operativo |
| BR-007 | Conciliar pagos y emitir tickets automáticamente al confirmarse | Must | reduce trabajo manual | `>= 85%` conciliación automática |
| BR-008 | Entregar analítica de ventas, ingresos y asistencia por evento | Should | mejora toma de decisiones | dashboard con KPIs por evento |
| BR-009 | Gestionar roles y permisos para admin, organizador, guardia y asistente | Must | seguridad y operación | RBAC activo para 4 roles |
| BR-010 | Detectar tickets duplicados, reenviados o reutilizados | Must | antifraude | incidentes auditados y bloqueo de reuso |
| BR-011 | Permitir personalización básica de landing y branding | Should | valor comercial para organizadores | colores, logo y banner configurables |
| BR-012 | Habilitar soporte conversacional y reenvío de tickets por WhatsApp | Could | conveniencia y retención | flujo documentado para fase siguiente |

## 12. Reglas de negocio y políticas

| ID | Regla | Tipo | Origen |
|----|-------|------|--------|
| RB-01 | Un ticket pertenece a un solo evento y a una sola orden confirmada | política | operación core |
| RB-02 | Un ticket usado no puede volver a ingresar salvo excepción autorizada | política | control de acceso |
| RB-03 | El ticket sólo se emite cuando el pago cambia a confirmado | política | integridad financiera |
| RB-04 | La app de guardias sólo puede descargar eventos asignados al usuario | política | seguridad operativa |
| RB-05 | Las órdenes pendientes deben expirar si no se confirma el pago dentro de la ventana definida | política | gestión de cupos |
| RB-06 | Todo escaneo debe generar un registro de auditoría con resultado | política | trazabilidad |
| RB-07 | Un organizador no puede ver ni editar eventos de otra organización | política | aislamiento multi-tenant |
| RB-08 | Todo QR debe validarse contra firma/estado y no sólo por apariencia visual | política | antifraude |

## 13. Supuestos, restricciones y dependencias

- **Supuestos**: el público objetivo usa smartphones; WhatsApp es un canal natural de soporte y compra; el pago QR tiene aceptación creciente; los organizadores toleran onboarding ligero si el valor es claro.
- **Restricciones**: equipo pequeño; presupuesto controlado; prioridad MVP; conectividad variable en eventos; necesidad de operar con proveedores externos para pagos y mensajería.
- **Dependencias**: integraciones bancarias o con pasarela QR; WhatsApp API; servicios de notificación; infraestructura cloud; almacenamiento seguro para tickets y auditoría.

## 14. Alcance de negocio

### 14.1 En alcance

- Dashboard administrativo.
- Gestión de eventos y tickets.
- Órdenes, pagos QR y emisión de tickets.
- Landing pública del evento.
- App operativa para guardias con offline.
- Validación QR y antifraude básico.
- Reportes operativos y de asistencia.

### 14.2 Fuera de alcance

- Marketplace y reventa oficial.
- Loyalty, membresías y gamificación.
- Pricing dinámico.
- IA predictiva de demanda.
- Integración completa con Seats.io en el primer release.

## 15. Beneficios esperados y business case resumido

| Tipo | Año 1 | Año 2 | Año 3 |
|------|-------|-------|-------|
| Ingresos por comisiones | USD 12,000 | USD 32,000 | USD 65,000 |
| Ingresos por planes premium | USD 4,800 | USD 14,400 | USD 28,800 |
| Servicios de setup / branding | USD 3,000 | USD 8,000 | USD 16,000 |
| Inversión inicial CAPEX | USD 7,500 | USD 2,000 | USD 2,000 |
| OPEX cloud + soporte + APIs | USD 5,400 | USD 9,600 | USD 16,800 |
| **Beneficio neto estimado** | **USD 6,900** | **USD 42,800** | **USD 91,000** |

> Estas cifras son estimaciones internas de negocio para priorización académica y deben validarse con pilotos y pricing real.

## 16. Riesgos de negocio

| Riesgo | Probabilidad | Impacto | Mitigación | Responsable |
|--------|--------------|---------|------------|-------------|
| Baja adopción inicial por parte de organizadores | media | alta | onboarding guiado y pilotos universitarios | founders |
| Dependencia de pasarela QR o banco | media | alta | capa de adaptadores y fallback manual asistido | producto/ingeniería |
| Fallas de internet en el evento | alta | alta | modo offline-first para guardias | ingeniería |
| Rechazo por dudas sobre seguridad del ticket | media | media | antifraude visible, branding y soporte | producto |
| Sobrecarga operativa en eventos masivos | media | alta | caché, colas y observabilidad | ingeniería |
| Riesgo regulatorio o contractual con proveedores | baja | media | revisión temprana de integraciones y SLA | founders |

## 17. Criterios de éxito del proyecto de negocio

- Cumplimiento de al menos 5 de 6 objetivos SMART del BRD.
- Tasa de fraude menor a 1% en eventos operados por la plataforma.
- Tiempo de validación mediano menor o igual a 3 segundos.
- Al menos 3 organizadores activos recurrentes después del piloto inicial.
- Satisfacción del organizador mayor o igual a 4/5.

## 18. Trazabilidad a documentos hijos

| BRD ID | MRD relacionado | PRD relacionado | Caso de uso FSD |
|--------|-----------------|-----------------|-----------------|
| BR-001 | MRD-N-01 | PRD-REQ-001, PRD-REQ-002 | FSD-UC-001 |
| BR-002 | MRD-N-02 | PRD-REQ-003, PRD-REQ-004 | FSD-UC-003, FSD-UC-004 |
| BR-003 | MRD-N-03 | PRD-REQ-005, PRD-REQ-006 | FSD-UC-005 |
| BR-004 | MRD-N-04 | PRD-REQ-009, PRD-REQ-010 | FSD-UC-008 |
| BR-005 | MRD-N-05 | PRD-REQ-011 | FSD-UC-007, FSD-UC-009 |
| BR-006 | MRD-N-06 | PRD-REQ-007 | FSD-UC-004, FSD-UC-005 |
| BR-007 | MRD-N-07 | PRD-REQ-008 | FSD-UC-005 |
| BR-008 | MRD-N-08 | PRD-REQ-013 | FSD-UC-010 |
| BR-009 | MRD-N-09 | PRD-REQ-014 | transversal |
| BR-010 | MRD-N-10 | PRD-REQ-012 | FSD-UC-008, FSD-UC-009 |
| BR-011 | MRD-N-11 | PRD-REQ-015 | FSD-UC-003 |
| BR-012 | MRD-N-12 | PRD-REQ-016 | FSD-UC-006 |

## 19. Aprobaciones

| Rol | Nombre | Firma | Fecha |
|-----|--------|-------|-------|
| Sponsor | Pendiente |  |  |
| Product Lead | Antonio Ovando |  | 13/05/2026 |
| Arquitectura | Carla Marcela Florida Roman |  | 13/05/2026 |

## 20. Registro de cambios

| Versión | Fecha | Autor | Cambio |
|---------|-------|-------|--------|
| v0.1 | 13/05/2026 | Antonio Ovando, Carla Marcela Florida Roman | Versión inicial del BRD para QrTicket |
