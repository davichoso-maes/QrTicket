# Guías UI/UX operativas — QrTicket

> Guías de interfaz y operación para QrTicket basadas en `CLAUDE.md`, el BRD/PRD/FSD y el contexto de eventos de alta presión.

## 0. Principios

| Principio | Implicación de diseño |
|-----------|----------------------|
| Velocidad operativa | acciones críticas con el menor número de pasos posible |
| Feedback inmediato | confirmaciones visuales y sonoras en validación |
| Claridad por encima de ornamento | textos, estados y decisiones visibles |
| Contraste alto en acceso | verde/rojo muy claros, tipografía grande, cámara full screen |
| Mobile-first real | compra y guardias priorizan pantallas pequeñas |
| Tiempo real visible | ventas, sync y validaciones deben mostrar estado actual |
| Baja ansiedad del usuario | estados y mensajes siempre explican qué pasó y qué sigue |

## 1. Sistema de color operativo

```ts
const qrticketPalette = {
  brand: {
    primary: '#0f766e',
    secondary: '#1d4ed8',
    accent: '#f59e0b',
  },
  access: {
    valid: '#16a34a',
    invalid: '#dc2626',
    warning: '#f59e0b',
    offline: '#2563eb',
  },
  payment: {
    pending: '#f59e0b',
    confirmed: '#16a34a',
    rejected: '#dc2626',
    expired: '#6b7280',
  },
  tickets: {
    active: '#0f766e',
    used: '#334155',
    refunded: '#7c3aed',
    cancelled: '#dc2626',
  },
};
```

## 2. Tipografía y tono visual

- Dashboard: tipografía sobria y legible, con jerarquía clara para KPIs.
- Landing pública: hero visual fuerte, CTA prominente y tarjetas de ticket simples.
- App guardias: texto grande, bordes amplios, cero ambigüedad.
- Estados del sistema: una palabra fuerte + explicación corta.

## 3. Layouts principales

### 3.1 Dashboard organizador

- Sidebar fija con módulos: Inicio, Eventos, Tickets, Pagos, Guardias, Reportes.
- Header con selector de organización y quick actions.
- Home con cards KPI, gráfica de ventas y tabla de eventos.

### 3.2 Landing pública

- Hero con banner, fecha, ciudad, CTA de compra.
- Sección de tickets con precio, cupo y beneficios.
- FAQ y soporte al final.
- CTA sticky en móvil.

### 3.3 App de guardias

- Pantalla 1: login y estado de conexión.
- Pantalla 2: eventos asignados y botón sincronizar.
- Pantalla 3: escaneo full screen con overlay simple.
- Pantalla 4: resultado grande con color y motivo.

## 4. Componentes recurrentes

### 4.1 KPI card

- Número principal grande.
- Variación vs periodo previo.
- Microtexto con definición del KPI.

### 4.2 Ticket card pública

- Nombre del ticket.
- Precio.
- Cupos o disponibilidad.
- Restricciones cortas.
- CTA comprar.

### 4.3 Payment status badge

- `Pendiente`, `Confirmado`, `Expirado`, `Rechazado`.
- Color obligatorio por estado.

### 4.4 Guardia scan result

- Verde: válido, nombre y ticket.
- Rojo: inválido, motivo exacto.
- Azul: modo offline / sincronización pendiente.

### 4.5 Sync banner

- Muestra modo online/offline.
- Última sincronización.
- Cantidad de pendientes por subir.

## 5. Pantallas críticas

### 5.1 Event builder

- Wizard ligero o formulario largo con secciones claras.
- Guardado progresivo.
- Estado visible `draft/active`.

### 5.2 Checkout móvil

- Máximo 3 bloques: ticket, datos, pago.
- QR de pago prominente.
- Estado de orden visible sin refresco manual complejo.

### 5.3 Scanner de guardias

- Cámara full screen.
- Indicador online/offline siempre visible.
- Vibración/sonido distintos para válido e inválido.
- Botón manual de sincronización accesible.

## 6. Accesibilidad y usabilidad

- Contraste mínimo AA en dashboard y móvil.
- No depender sólo del color: siempre acompañar con texto/icono.
- Tappable areas grandes en guardias.
- Mensajes de error accionables, no técnicos.

## 7. Anti-patrones a evitar

- Esconder el estado de una orden o pago.
- Mezclar demasiados datos en la pantalla de guardias.
- Colores débiles para válido/inválido.
- Checkouts con formularios largos y ambiguos.
- Gráficas complejas antes de resolver KPIs esenciales.

## 8. Registro de cambios

| Versión | Fecha | Autor | Cambio |
|---------|-------|-------|--------|
| v0.1 | 13/05/2026 | Equipo QrTicket | Guía inicial de UI/UX operativa |
