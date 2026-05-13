# Market Requirements Document — QrTicket

> Documento de requisitos de mercado para QrTicket, basado en [docs/brd/BRD_v0.1.md](../brd/BRD_v0.1.md) y estructurado con [templates/MRD_TEMPLATE.md](../../templates/MRD_TEMPLATE.md).

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
| Product Manager / Autor | Equipo QrTicket |
| Revisores | Docente + stakeholders |
| Estado | Borrador |
| Relación con BRD | `docs/brd/BRD_v0.1.md` |

## 1. Resumen ejecutivo

QrTicket compite en un mercado donde el problema no es la ausencia de eventos, sino la baja madurez operativa de su gestión. El segmento inicial objetivo es el de eventos universitarios y académicos bolivianos, donde el organizador necesita una solución accesible, rápida y confiable, y el asistente espera una experiencia similar a los productos digitales que ya usa a diario: celular, QR y WhatsApp. La oportunidad comercial está en ofrecer ticketing digital local-first, integrado a pagos QR y preparado para conectividad inestable.

La diferenciación del producto no depende únicamente de vender tickets, sino de resolver el ciclo completo: descubrimiento, compra, pago, emisión, acceso, conciliación y reporte. El mercado objetivo inmediato es menor que el del ticketing regional generalista, pero tiene mejores condiciones para penetración inicial por frecuencia de eventos, repetición de organizadores y dolor operativo no resuelto. QrTicket puede posicionarse como la solución mejor adaptada a Bolivia para eventos universitarios y luego expandirse a conciertos, festivales y eventos corporativos.

## 2. Visión del producto

> Para organizadores y asistentes de eventos bolivianos que hoy dependen de procesos manuales, QrTicket es una plataforma de ticketing QR con pagos locales y operación offline que profesionaliza el evento sin aumentar la fricción.

## 3. Análisis de mercado

### 3.1 Tamaño de mercado

| Métrica | Valor | Fuente |
|---------|-------|--------|
| TAM | Mercado boliviano de entradas y registros pagos para eventos urbanos y universitarios: estimación interna `Bs 35M–60M/año` | estimación inicial del equipo; validar en discovery |
| SAM | Segmento atendible en universidades, congresos, festivales medianos y eventos de ciudad: `Bs 12M–18M/año` | estimación inicial del equipo |
| SOM | Captura objetivo del release expandido: `60–90 eventos/año`, `35k–50k tickets/año`, GMV estimado `Bs 1.2M–2.4M/año` | hipótesis de entrada a mercado |

> Los valores de TAM/SAM/SOM son hipótesis de trabajo para priorización y deben ser refinados con entrevistas, pilotos y benchmark comercial.

### 3.2 Tendencias del sector

- **Predominio del pago QR**: los usuarios bolivianos ya están familiarizados con transferencias y pagos QR como alternativa al efectivo.
- **WhatsApp como interfaz natural**: para muchos usuarios, WhatsApp es más accesible que descargar una app o entrar a un portal complejo.
- **Eventos con operación híbrida**: los organizadores combinan venta digital con validación presencial y requieren sincronización entre ambos mundos.
- **Sensibilidad al fraude**: reenviar comprobantes, usar capturas o falsificar tickets sigue siendo un temor recurrente.
- **Infraestructura variable**: la conectividad en recintos y campus obliga a diseñar offline-first para validación.

### 3.3 Factores regulatorios y de cumplimiento

- Ley 164 de telecomunicaciones y TIC en Bolivia como referencia general de entorno digital.
- Obligaciones de seguridad contractual con bancos, pasarelas y proveedores de mensajería.
- Buenas prácticas de protección de datos personales, auditoría y seguridad de transacciones.
- Términos y condiciones de recintos, universidades y organizadores para emisión, cancelación y reembolsos.

## 4. Segmentación y personas

### 4.1 Segmentos de clientes

| Segmento | Tamaño relativo | Necesidad principal | Disposición a pagar |
|----------|-----------------|---------------------|---------------------|
| Centros de estudiantes y sociedades científicas | alta | vender y controlar accesos con poco equipo | media |
| Universidades y unidades académicas | media | ordenar eventos institucionales y reportar asistencia | media-alta |
| Productoras y promotores medianos | media | operar tickets con branding y control robusto | alta |
| Organizadores corporativos | baja-media | invitados, acceso y reporting confiable | alta |

### 4.2 Personas

#### Persona 1 — Carlos, organizador universitario

- **Rol**: líder de centro de estudiantes o comité organizador.
- **Demografía**: 20-30 años, alta afinidad móvil, baja formalización operativa.
- **Objetivos**: lanzar eventos rápido, vender cupos, validar ingresos, demostrar resultados.
- **Dolores actuales**: conciliación manual, desorden con listas, tickets reenviados, presión el día del evento.
- **Comportamiento digital**: usa WhatsApp, Instagram, Google Forms, Excel y banca móvil.
- **Frase representativa**: "No necesito más herramientas; necesito que el evento no se me salga de las manos".

#### Persona 2 — María, asistente compradora

- **Rol**: estudiante o joven profesional que compra entradas desde el celular.
- **Demografía**: 18-29 años, digital-first, valora inmediatez.
- **Objetivos**: pagar fácil, confirmar rápido, guardar ticket, entrar sin problema.
- **Dolores actuales**: mensajes cruzados, validación manual, tickets perdidos, incertidumbre sobre el estado del pago.
- **Comportamiento digital**: WhatsApp, Instagram, apps bancarias, correo poco frecuente.
- **Frase representativa**: "Si me toma mucho tiempo comprar, lo dejo para después o ya no voy".

#### Persona 3 — Diego, guardia operativo

- **Rol**: validador de accesos en puerta.
- **Objetivos**: escanear rápido, evitar discusiones y seguir operando sin señal.
- **Dolores actuales**: listas desactualizadas, descoordinación, presión en pico de ingreso.
- **Comportamiento digital**: uso funcional del celular, poca paciencia para flujos complejos.
- **Frase representativa**: "Necesito ver verde o rojo y seguir".

#### Persona 4 — Ana, manager de eventos recurrentes

- **Rol**: organizadora semi-profesional con varios eventos al año.
- **Objetivos**: branding, reportes, control de staff, crecimiento comercial.
- **Dolores actuales**: herramientas caseras que no escalan y poca visibilidad del negocio.
- **Frase representativa**: "Quiero dejar de operar como si cada evento empezara de cero".

## 5. Jobs-to-be-Done

| JTBD ID | Cuando… | Quiero… | Para poder… |
|---------|---------|---------|-------------|
| JTBD-01 | voy a lanzar un evento | crear y publicar el evento en minutos | empezar a vender sin depender de diseño y Excel |
| JTBD-02 | un asistente me escribe por WhatsApp | ofrecerle una compra guiada | cerrar la venta sin conversación manual larga |
| JTBD-03 | una persona quiere comprar una entrada | mostrarle tickets, cupos y precio claros | reducir abandono |
| JTBD-04 | el usuario paga con QR | confirmar el pago y emitir ticket automáticamente | evitar conciliación manual |
| JTBD-05 | llega el día del evento | validar QR en segundos | reducir filas y discusiones |
| JTBD-06 | se cae internet en puerta | seguir escaneando igual | no frenar el ingreso |
| JTBD-07 | termina el evento | ver asistencia real e ingresos | aprender y justificar resultados |
| JTBD-08 | un asistente pierde su ticket | reenviarlo o recuperarlo fácil | evitar soporte manual caótico |

## 6. Análisis competitivo

### 6.1 Tabla comparativa

| Criterio | QrTicket | Eventbrite | Passline | Boletería manual | Google Forms + Excel |
|----------|----------|------------|----------|------------------|----------------------|
| Adaptación a Bolivia | alta | baja-media | media | alta | alta |
| Pagos QR locales | alta | baja | media | media | baja |
| Operación offline guardias | alta | baja | baja-media | n/a | n/a |
| Canal WhatsApp | alta | baja | baja | alta manual | alta manual |
| Analítica por evento | media-alta | alta | media | baja | baja |
| Facilidad de arranque | media | alta | media | media | alta |
| Antifraude QR | alta | media-alta | media | baja | baja |
| Foco universitario | alta | baja | baja | media | media |

### 6.2 Positioning statement

> Para organizadores bolivianos que hoy venden y validan entradas con procesos manuales, QrTicket es una plataforma de ticketing QR local-first que integra pagos QR, validación offline y automatización conversacional, a diferencia de alternativas genéricas que no resuelven la operación real del evento en Bolivia.

### 6.3 Ventaja competitiva sostenible

- Integración de operación online y offline en un solo ecosistema.
- Ajuste fino al mercado boliviano en métodos de pago y hábitos de compra.
- Capacidad de entrar al mercado universitario con ciclo de venta corto y alta repetición.
- Barrera operativa: una vez que el organizador confía el acceso y la conciliación al sistema, el switching cost crece.

## 7. Propuesta de valor

### 7.1 Value proposition canvas resumido

| Gains | Pains | Gain creators | Pain relievers | Products & services |
|-------|-------|----------------|----------------|---------------------|
| Más ventas digitales | Filas y abandono | compra multicanal | checkout simple | landing + checkout |
| Mayor confianza | tickets duplicados | QR único y trazabilidad | validación server-side | ticket QR inteligente |
| Menos trabajo manual | conciliación lenta | webhook + emisión automática | estado de pago claro | payments engine |
| Operación continua | mala señal en recintos | modo offline | dataset local y sync | app guardias |
| Mejor toma de decisiones | no hay métricas | dashboards y reportes | KPIs por evento | analytics dashboard |

## 8. Pricing y modelo de negocio

- **Modelo principal**: comisión por ticket vendido.
- **Modelo secundario**: suscripción mensual para organizadores con eventos recurrentes.
- **Servicios complementarios**: branding, setup operativo, soporte premium el día del evento.
- **Rango propuesto inicial**:
  - comisión base: `3%–6%` por ticket;
  - plan recurrente: `USD 19–49/mes` según volumen;
  - setup de evento especial: `USD 50–250`.
- **Benchmark cualitativo**: competir por valor operativo local, no por ser la opción más barata en abstracto.

## 9. Go-to-market

### 9.1 Canales de adquisición

- **Directo**: demos a centros de estudiantes, sociedades científicas y organizadores.
- **Digital**: contenido en redes, casos reales, campañas en Instagram/TikTok/Meta Ads.
- **Partners**: universidades, recintos, productoras, promotores y comunidades estudiantiles.
- **Referidos**: organizadores satisfechos que recomiendan a otros comités.

### 9.2 Estrategia de lanzamiento

- **Pre-launch**: pilotos con 2-3 organizadores universitarios.
- **Launch**: release 1.0.0 con eventos de ticketing simple, pagos QR y guardias offline.
- **Post-launch**: paquetes de onboarding, soporte activo y expansión a eventos semicomerciales.

### 9.3 Funnel AARRR inicial

| Etapa | Métrica | Meta |
|-------|---------|------|
| Acquisition | organizadores contactados por mes | `>= 30` |
| Activation | organizadores que crean su primer evento | `>= 10/mes` |
| Retention | organizadores que repiten evento en 90 días | `>= 40%` |
| Revenue | GMV mensual procesado | `>= Bs 100k` en fase temprana |
| Referral | organizadores referidos por otros | `>= 20%` del pipeline |

## 10. Métricas de éxito del producto

- **North Star Metric**: asistentes validados exitosamente por minuto sin incidentes críticos.
- **KPIs secundarios**:
  - conversión de compra `>= 12%`;
  - tiempo de emisión post-pago `<= 30 s`;
  - tasa de sincronización offline exitosa `>= 95%`;
  - tasa de abandono de checkout `< 25%`;
  - NPS organizador `>= 40` en piloto.

## 11. Requerimientos de mercado (alto nivel)

| ID | Requerimiento | Prioridad | Justificación |
|----|---------------|-----------|---------------|
| MRD-N-01 | El mercado necesita autogestión de eventos con baja curva de aprendizaje | Must | el organizador no tiene equipo técnico |
| MRD-N-02 | El mercado exige compra simple desde web y móvil | Must | el asistente abandona flujos complejos |
| MRD-N-03 | El ticket debe ser digital, único y confiable | Must | el fraude es una preocupación central |
| MRD-N-04 | La validación debe ser rápida y visible | Must | la puerta define la experiencia del evento |
| MRD-N-05 | La app de guardias debe seguir operando sin internet | Must | la conectividad del recinto es variable |
| MRD-N-06 | El pago QR debe sentirse local y familiar | Must | es el método más natural del mercado |
| MRD-N-07 | El mercado valora conciliación automática y emisión inmediata | Must | ahorra tiempo al organizador |
| MRD-N-08 | Los organizadores esperan métricas por evento | Should | ayuda a justificar decisiones y presupuesto |
| MRD-N-09 | El sistema debe separar roles con permisos claros | Must | protege la operación multiusuario |
| MRD-N-10 | El mercado castiga cualquier sensación de ticket inseguro | Must | la confianza es parte del producto |
| MRD-N-11 | La landing debe ayudar a vender, no sólo informar | Should | impacta conversión |
| MRD-N-12 | WhatsApp debe integrarse al soporte y recuperación del ticket | Should | es el canal de menor fricción |

## 12. Supuestos e hipótesis a validar

| ID | Hipótesis | Cómo validar | Criterio de éxito |
|----|-----------|--------------|-------------------|
| H1 | Los organizadores universitarios pagarán comisión si el sistema reduce fraude y trabajo manual | entrevistas + piloto | `>= 4/5` organizadores aceptan comisión |
| H2 | El pago QR aumenta la tasa de cierre frente a transferencia manual | A/B en piloto | mejora relativa `>= 15%` |
| H3 | La operación offline es decisiva en la elección del producto | entrevistas con guardias y organizadores | `>= 70%` la considera crítica |
| H4 | WhatsApp acelera recuperación de tickets y soporte | flujo piloto | reducción del tiempo de soporte `>= 40%` |
| H5 | El organizador valora más la confiabilidad operativa que un diseño muy sofisticado | discovery + shadowing | prioridad declarada por mayoría |
| H6 | El segmento universitario puede abrir expansión posterior a productoras medianas | seguimiento comercial | al menos 2 leads fuera del campus en 3 meses |

## 13. Riesgos de mercado

| Riesgo | Prob. | Impacto | Mitigación |
|--------|-------|---------|------------|
| Competidor regional entra con pricing agresivo | media | alto | enfocarse en adaptación local y operación offline |
| El mercado percibe alto riesgo en pagos digitales | media | medio | reforzar confianza, soporte y estados visibles |
| Los organizadores siguen prefiriendo procesos manuales por costumbre | media | alto | pilotos con quick wins y casos reales |
| Bancos/pasarelas dificultan integración estable | media | alto | capa de abstractions y roadmap incremental |
| La compra por WhatsApp no despega como canal transaccional completo | baja-media | medio | iniciar por soporte/recovery y luego escalar a venta completa |

## 14. Trazabilidad

| MRD ID | BRD ID | PRD ID |
|--------|--------|--------|
| MRD-N-01 | BR-001 | PRD-REQ-001 |
| MRD-N-02 | BR-002 | PRD-REQ-003 |
| MRD-N-03 | BR-003 | PRD-REQ-005 |
| MRD-N-04 | BR-004 | PRD-REQ-009 |
| MRD-N-05 | BR-005 | PRD-REQ-011 |
| MRD-N-06 | BR-006 | PRD-REQ-007 |
| MRD-N-07 | BR-007 | PRD-REQ-008 |
| MRD-N-08 | BR-008 | PRD-REQ-013 |
| MRD-N-09 | BR-009 | PRD-REQ-014 |
| MRD-N-10 | BR-010 | PRD-REQ-012 |
| MRD-N-11 | BR-011 | PRD-REQ-015 |
| MRD-N-12 | BR-012 | PRD-REQ-016 |

## 15. Anexos

- Supuestos de sizing inicial del mercado.
- Lista de hipótesis a validar en los primeros pilotos.
- Glosario comercial del dominio de ticketing boliviano.

## 16. Registro de cambios

| Versión | Fecha | Autor | Cambio |
|---------|-------|-------|--------|
| v0.1 | 13/05/2026 | Equipo QrTicket | Versión inicial del MRD |
