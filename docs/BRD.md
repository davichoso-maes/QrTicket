
# Business Requirements Document (BRD) – QrTicket

## 0. Metadatos

| Campo | Valor |
|-------|-------|
| Producto | QrTicket |
| Grupo | GXX |
| Versión | v3.0 |
| Fecha | 02/05/2026 |
| Sponsor de negocio | Organizador universitario UMSS |
| Stakeholders | Organizadores, estudiantes, equipo desarrollo, bancos, universidades |
| Autores | Equipo QrTicket |
| Revisores | Docente + grupo par |
| Estado | Borrador |

## 1. Resumen ejecutivo

Los procesos actuales de gestión de eventos en Bolivia presentan fricción significativa: filas presenciales, pagos manuales y validación ineficiente. QrTicket digitaliza el flujo completo mediante pagos QR, venta multicanal y validación en tiempo real.

Se proyecta reducir el tiempo de compra en 70%, aumentar la conversión en 30% y gestionar 120 eventos el primer año. Se requiere aprobación para desarrollar MVP.

## 2. Contexto del negocio

- Organización: Startup QrTicket
- Unidad impactada: Gestión de eventos
- Procesos: registro, pagos, control acceso
- Estrategia: digitalización eventos Bolivia

## 3. Problema y oportunidad

### Problema
Más del 40% de usuarios reportan filas como principal fricción. Procesos manuales generan errores y baja conversión.

### Oportunidad
Automatización completa, aumento ingresos y mejor experiencia.

## 4. Usuarios

### Persona principal
Estudiante universitario  
Jobs: comprar, pagar, asistir  
Dolor: filas, procesos lentos  
Ganancia: rapidez y seguridad  

### Persona secundaria
Organizador  
Jobs: crear evento, vender, controlar acceso  
Dolor: desorden, conciliación  
Ganancia: automatización  

## 5. Propuesta de valor

Compra, paga y entra sin filas mediante QR y WhatsApp.

## 6. Panorama competitivo

| Competidor | Tipo | Fortaleza | Debilidad |
|-----------|------|----------|----------|
| Todotix | directo | UX | complejo |
| Passline | directo | escala | no adaptado |
| Manual | indirecto | simple | ineficiente |

## 7. Business Model Canvas

| Bloque | Elementos |
|--------|----------|
| Segmentos | estudiantes / organizadores / productoras |
| Propuesta | sin filas / QR / automatización |
| Canales | web / app / WhatsApp |
| Relación | autoservicio / soporte / onboarding |
| Ingresos | freemium / upsell / servicios |
| Recursos | software / servidores / equipo |
| Actividades | desarrollo / soporte / ventas |
| Socios | bancos / universidades / pasarelas |
| Costos | infraestructura / marketing / desarrollo |

## 8. Métricas

| ID | KPI | North Star | Línea base | Meta | Horizonte | Fuente |
|----|-----|-----------|------------|------|-----------|--------|
| KPI1 | eventos gestionados | sí | 0 | 120 | 1 año | sistema |
| KPI2 | tiempo compra | no | 10 min | <1 min | 1 año | encuesta |
| KPI3 | pagos QR | no | 20% | 60% | 1 año | sistema |

## 9. Objetivos SMART

| ID | Objetivo | Métrica | Base | Meta | Horizonte |
|----|----------|--------|------|------|-----------|
| BO1 | aumentar eventos | cantidad | 0 | 120 | 1 año |
| BO2 | reducir tiempo | minutos | 10 | 1 | 1 año |
| BO3 | digitalizar pagos | % | 20 | 60 | 1 año |

## 10. Stakeholders (RACI)

| Stakeholder | Interés | R/A/C/I |
|-------------|---------|--------|
| Sponsor | estratégico | A |
| Desarrollo | ejecución | R |
| Usuarios | experiencia | C |
| Bancos | integración | I |

## 11. Requerimientos

| ID | Req | Prioridad | Justificación | Métrica |
|----|-----|----------|--------------|--------|
| BR1 | compra digital | Must | eliminar filas | 80% digital |
| BR2 | pago QR | Must | eficiencia | 60% uso |
| BR3 | ticket QR | Must | automatización | 100% automático |
| BR4 | validación acceso | Must | antifraude | 0 duplicados |
| BR5 | app guardias | Must | operación | uso en eventos |
| BR6 | reportes | Should | decisiones | dashboards |
| BR7 | multicanal | Should | accesibilidad | 3 canales |
| BR8 | notificaciones | Could | UX | confirmaciones |

## 12. Reglas

| ID | Regla | Tipo | Origen |
|----|------|------|--------|
| RB1 | ticket único | negocio | sistema |
| RB2 | pago previo | negocio | sistema |
| RB3 | QR válido | técnico | sistema |

## 13. Supuestos y restricciones

- Supuestos: uso smartphone, internet
- Restricciones: Bolivia, QR bancario, bajo presupuesto
- Dependencias: bancos, APIs

## 14. Alcance

Incluye: pagos, venta, acceso  
Excluye: marketing

## 15. Business case

| Tipo | Año 1 |
|------|------|
| Ingresos | 0 |
| Costos | 5000 USD |
| ROI | negativo (fase inversión) |

## 16. Riesgos

| Riesgo | Prob | Impacto | Mitigación |
|--------|------|--------|-----------|
| baja adopción | media | alta | marketing |
| fallos | baja | alta | infraestructura |

## 17. Criterios de éxito

- ≥120 eventos
- ≥60% pagos QR
- satisfacción >4/5

