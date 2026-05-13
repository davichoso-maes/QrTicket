# AGENTS.md — QrTicket

## 1. Visión General del Sistema

QrTicket es una plataforma integral de gestión de eventos, venta de entradas digitales y control de acceso mediante QR, diseñada inicialmente para el mercado boliviano y especialmente orientada al ecosistema universitario.

El sistema nace para resolver problemas operativos, administrativos y de experiencia de usuario presentes en la organización de eventos académicos, culturales, sociales y masivos.

La plataforma contempla:

- Gestión de eventos.
- Venta multicanal de entradas.
- Tickets digitales con QR dinámico.
- Validación de acceso en tiempo real.
- Operación offline para guardias.
- Pagos mediante QR bancario.
- Automatización conversacional mediante WhatsApp.
- Dashboard SaaS administrativo.
- Aplicaciones móviles operativas.
- Escalabilidad para eventos de alta concurrencia.

QrTicket debe ser concebido como un ecosistema modular, escalable y orientado a tiempo real.

---

# 2. Problema que Resuelve

El contexto boliviano y universitario presenta múltiples problemas operativos:

## Problemas del Usuario Final (Asistente)

- Procesos manuales.
- Filas para pago.
- Inscripción burocrática.
- Información dispersa.
- Desconfianza en pagos digitales.
- Tickets falsificados.
- Mala organización en accesos.
- Falta de soporte rápido.
- Experiencias lentas y estresantes.

## Problemas del Organizador

- Conciliación manual de pagos.
- Registro fragmentado.
- Control deficiente de asistentes.
- Dificultad para validar accesos.
- Riesgo de fraude.
- Falta de métricas.
- Operación improvisada.
- Dependencia excesiva de hojas de cálculo.
- Dificultad para escalar eventos.
- Falta de herramientas profesionales.

## Problemas Operativos en Eventos

- Saturación en ingresos.
- Tickets duplicados.
- Mala coordinación de guardias.
- Caídas de internet.
- Falta de sincronización.
- Ausencia de datos en tiempo real.
- Imposibilidad de medir flujo de acceso.

QrTicket existe para eliminar estos problemas mediante automatización, digitalización y operación en tiempo real.

---

# 3. Objetivo del Producto

Crear una plataforma moderna, confiable y altamente operativa para:

- Gestionar eventos.
- Vender entradas.
- Controlar accesos.
- Automatizar pagos.
- Reducir fricción.
- Escalar eventos.
- Minimizar fraude.
- Mejorar la experiencia del asistente.
- Profesionalizar la gestión de eventos universitarios y masivos.

---

# 4. Propuesta de Valor

## Principales Diferenciadores

### 4.1 Venta Multicanal

El usuario puede comprar entradas desde:

- Web.
- Aplicación móvil.
- WhatsApp.

Esto elimina barreras de acceso.

---

### 4.2 Tickets QR Inteligentes

Cada ticket posee:

- QR único.
- Validación en tiempo real.
- Estado dinámico.
- Protección antifraude.
- Historial de uso.
- Asociación a usuario.
- Asociación a evento.
- Asociación a tipo de entrada.

---

### 4.3 Operación Offline para Guardias

Uno de los pilares críticos del sistema.

La app de guardias debe seguir funcionando incluso sin internet.

Características:

- Base SQLite local.
- Sincronización incremental.
- Cache de tickets válidos.
- Validación offline.
- Reconciliación posterior.
- Prevención de doble acceso.
- Sincronización manual.

---

### 4.4 Integración con QR Bancario

El sistema está adaptado al contexto boliviano.

Debe integrarse con:

- QR Simple.
- Bancos bolivianos.
- Libélula.
- BNB.
- Unión.
- Tigo Money.
- Pasarelas futuras.

---

### 4.5 Automatización Conversacional

WhatsApp actúa como canal de venta.

La IA interpreta intención mediante NLP.

Ejemplo:

"Quiero comprar 2 entradas VIP para el evento de medicina"

El sistema debe:

1. Interpretar intención.
2. Identificar evento.
3. Identificar ticket.
4. Generar orden.
5. Generar QR de pago.
6. Esperar confirmación bancaria.
7. Emitir ticket.
8. Enviar ticket automáticamente.

---

# 5. Público Objetivo

## Público Primario

- Universidades.
- Sociedades científicas.
- Centros de estudiantes.
- Organizadores universitarios.

## Público Secundario

- Conciertos.
- Festivales.
- Eventos corporativos.
- Eventos deportivos.
- Conferencias.
- Seminarios.
- Eventos culturales.

---

# 6. Arquitectura General del Ecosistema

QrTicket se compone de múltiples aplicaciones.

## 6.1 Dashboard Web Administrativo

Aplicación principal SaaS.

Usada por:

- Organizadores.
- Managers.
- Superadmins.

Responsabilidades:

- Gestión de eventos.
- Gestión de tickets.
- Gestión de pagos.
- Gestión de usuarios.
- Gestión de guardias.
- Reportes.
- Configuración.
- Analítica.
- Control operativo.

---

## 6.2 Aplicación Móvil de Guardias

Aplicación enfocada exclusivamente en operación.

Objetivos:

- Escaneo rápido.
- Validación instantánea.
- Fluidez operativa.
- Operación offline.
- Mínima complejidad.

---

## 6.3 Aplicación Móvil de Asistentes

Funciones:

- Compra de entradas.
- Wallet digital.
- Historial.
- Tickets.
- Perfil.
- Notificaciones.
- Eventos guardados.
- QR personal.

---

## 6.4 WhatsApp Bot

Canal automatizado.

Funciones:

- Consulta de eventos.
- Compra de tickets.
- Generación QR.
- Soporte.
- Confirmación de pagos.
- Reenvío de tickets.

---

## 6.5 Backend Central

Responsable de:

- Autenticación.
- APIs.
- Reglas de negocio.
- Validación.
- Tickets.
- Pagos.
- Integraciones.
- Seguridad.
- Sincronización.
- Webhooks.
- Reportería.

---

# 7. Stack Tecnológico

## Frontend Web

- Next.js.
- React.
- TypeScript.
- TailwindCSS.
- Shadcn/UI.
- React Query.
- Zustand o Redux.

---

## Backend

- Next.js API Routes o arquitectura modular.
- TypeScript.
- PostgreSQL.
- Prisma ORM.
- WebSockets.
- Queue system.

---

## Aplicaciones Móviles

- React Native.
- Expo o Native CLI.
- SQLite.
- Cámara nativa.
- Offline sync.

---

## Base de Datos

### Principal

- PostgreSQL.

### Local Offline

- SQLite.

---

## IA / NLP

- Gemini Light.
- NLP para WhatsApp.
- Clasificación de intención.
- Extracción de entidades.

---

## Infraestructura

Idealmente:

- Vercel.
- Railway.
- Supabase.
- AWS.
- Cloudflare.
- Docker.

---

# 8. Roles del Sistema

## 8.1 Super Administrador

Rol administrativo global.

Permisos:

- Crear managers.
- Crear organizadores.
- Gestionar recintos.
- Configuración global.
- Gestión de branding.
- Auditoría.
- Gestión de pasarelas.
- Gestión de límites.
- Ver métricas globales.

---

## 8.2 Manager / Organizador

Usuario operativo principal.

Permisos:

- Crear eventos.
- Editar eventos.
- Publicar eventos.
- Gestionar tickets.
- Ver pagos.
- Ver asistentes.
- Asignar guardias.
- Ver reportes.
- Configurar branding.
- Gestionar landing.

---

## 8.3 Guardias

Usuario operativo móvil.

Permisos:

- Login.
- Acceso a eventos asignados.
- Escaneo QR.
- Validación.
- Visualización mínima.

No deben tener acceso administrativo.

---

## 8.4 Asistentes

Usuarios compradores.

Funciones:

- Comprar tickets.
- Descargar tickets.
- Ver historial.
- Ver eventos.
- Acceder al evento.

---

# 9. Módulos Principales

# 9.1 Dashboard Inicio

Vista principal estadística.

Debe incluir:

## KPIs

- Eventos activos.
- Tickets vendidos.
- Ingresos.
- Conversión.
- Asistencia.
- Eventos finalizados.

## Gráficas

- Ventas por día.
- Ingresos.
- Conversión.
- Accesos.
- Tickets vendidos.

## Componentes

- Cards.
- Tabla de eventos.
- Actividad reciente.
- Alertas.
- Quick actions.

---

# 9.2 Gestión de Eventos

Módulo central.

## Funciones

- Crear evento.
- Editar.
- Duplicar.
- Publicar.
- Despublicar.
- Cancelar.
- Finalizar.

## Estados

- Draft.
- Activo.
- Agotado.
- Finalizado.
- Cancelado.

---

# 9.3 Configuración de Tickets

Dos modalidades.

## A) Configuración Simple

Ideal para:

- Eventos universitarios.
- Seminarios.
- Workshops.

Permite:

- General.
- VIP.
- VIP 1.
- VIP 2.
- Early Bird.
- Estudiante.

Cada ticket tiene:

- Precio.
- Capacidad.
- Cupos.
- Color.
- Horario.
- Restricciones.

---

## B) Configuración Avanzada con Seats.io

Para:

- Conciertos.
- Teatros.
- Eventos numerados.

Funciones:

- Mapa interactivo.
- Selección de asientos.
- Zonas.
- Ocupación.
- Estados.
- Pricing por sección.

---

# 9.4 Landing Pública del Evento

Cada evento tiene una landing pública.

Debe incluir:

- Banner.
- Información.
- Descripción.
- Fecha.
- Ubicación.
- Tickets.
- Capacidad.
- Expositores.
- Temario.
- Botón comprar.
- Redes.
- FAQ.

---

# 9.5 Gestión de Pagos

## Funciones

- Registro de transacciones.
- Confirmación bancaria.
- Webhooks.
- Conciliación.
- Estados.
- Reembolsos.

## Estados de Pago

- Pendiente.
- Confirmado.
- Rechazado.
- Expirado.
- Reembolsado.

## Métodos

- QR.
- Visa.
- Libélula.
- Tigo Money.
- Transferencia.

---

# 9.6 Sistema de Tickets

## Ticket contiene

- ID único.
- QR.
- Usuario.
- Evento.
- Tipo.
- Estado.
- Timestamp.
- Metadata.

## Estados

- Activo.
- Usado.
- Reembolsado.
- Cancelado.
- Expirado.

---

# 9.7 Control de Acceso

Uno de los módulos críticos.

## Funciones

- Escaneo.
- Validación.
- Revalidación.
- Alertas.
- Detección fraude.
- Sincronización.
- Métricas.

## Validaciones

- QR válido.
- Evento correcto.
- Ticket activo.
- Ticket no usado.
- Horario válido.
- Puerta válida.

---

# 9.8 Gestión de Guardias

## Funciones

- Crear guardias.
- Asignar eventos.
- Activar/desactivar.
- Ver historial.
- Gestionar credenciales.

## Datos

- Nombre.
- CI.
- Teléfono.
- Estado.
- Eventos.
- Historial.

---

# 9.9 Gestión de Usuarios

## Tipos

- Asistentes.
- Organizadores.
- Guardias.
- Admins.

## Funciones

- Activar.
- Desactivar.
- Editar.
- Roles.
- Permisos.
- Auditoría.

---

# 9.10 Reportes

Los reportes son event-centric.

## Métricas

- Ingresos.
- Conversión.
- Horas pico.
- Puertas.
- Tickets usados.
- No-shows.
- Guardias.
- Flujo de ingreso.

## Visualizaciones

- Line charts.
- Bar charts.
- Heatmaps.
- KPIs.
- Funnels.

---

# 10. Flujo de Compra

## Web/App

1. Usuario selecciona evento.
2. Selecciona ticket.
3. Ingresa datos.
4. Genera orden.
5. Genera QR.
6. Usuario paga.
7. Banco confirma.
8. Sistema emite ticket.
9. Ticket enviado.

---

# 11. Flujo WhatsApp

1. Usuario escribe.
2. IA interpreta.
3. Se identifica evento.
4. Se identifica ticket.
5. Se genera orden.
6. Se genera QR.
7. Usuario paga.
8. Webhook confirma.
9. Ticket enviado.

---

# 12. Flujo de Validación

1. Guardia inicia sesión.
2. Descarga evento.
3. Escanea QR.
4. Sistema valida.
5. Marca ticket.
6. Sincroniza.

---

# 13. Arquitectura de Datos

## Entidades Principales

### Users

- id
- name
- email
- phone
- role
- status
- createdAt

---

### Events

- id
- title
- slug
- description
- banner
- location
- capacity
- startDate
- endDate
- status
- organizerId

---

### Tickets

- id
- qr
- eventId
- userId
- type
- status
- metadata
- usedAt

---

### Payments

- id
- userId
- eventId
- amount
- method
- status
- transactionReference

---

### Guards

- id
- userId
- active
- assignedEvents

---

### AccessLogs

- id
- ticketId
- guardId
- gate
- scannedAt
- result

---

# 14. UX/UI Guidelines

## Principios

- Minimalismo.
- Alta legibilidad.
- Tiempo real.
- Baja fricción.
- Operación rápida.
- Acciones visibles.
- Responsive.
- Feedback inmediato.

---

## Estética

Inspiraciones:

- Stripe.
- Linear.
- Notion.
- Vercel.
- Framer.

---

## Componentes

- Sidebar.
- Topbar.
- Cards.
- Tables.
- Modals.
- Drawers.
- Tabs.
- Dropdowns.
- Badges.
- Toasts.
- Charts.

---

# 15. Diseño de la App de Guardias

## Objetivo

Velocidad operativa.

## Pantallas

### Login

- Usuario.
- Password.
- Estado conexión.

---

### Eventos asignados

- Lista.
- Estado sync.
- Descarga.

---

### Escaneo

Pantalla principal.

Debe tener:

- Cámara fullscreen.
- Feedback inmediato.
- Vibración.
- Sonido.
- Estado online/offline.

---

### Resultado válido

- Verde.
- Nombre.
- Ticket.
- Hora.

---

### Resultado inválido

- Rojo.
- Motivo.
- Ticket usado.
- Ticket inválido.
- Evento incorrecto.

---

# 16. Offline First

Uno de los requerimientos más importantes.

## Razón

Los eventos pueden:

- Perder internet.
- Saturar red móvil.
- Tener miles de usuarios.

## Estrategia

- SQLite local.
- Descarga previa.
- Sync incremental.
- Batch updates.
- Eventual consistency.

---

# 17. Seguridad

## Requerimientos

- JWT.
- Roles.
- Refresh tokens.
- Encriptación.
- HTTPS.
- Protección QR.
- Anti replay.
- Rate limiting.
- Logs.

---

# 18. Sistema Antifraude

## Debe detectar

- Tickets duplicados.
- QR alterados.
- Reuso.
- Acceso simultáneo.
- Capturas reutilizadas.

## Estrategias

- QR dinámico.
- Estado server-side.
- Timestamp.
- Hash.
- Invalidación inmediata.

---

# 19. Escalabilidad

El sistema debe soportar:

- Eventos pequeños.
- Eventos masivos.
- Miles de accesos simultáneos.
- Alta concurrencia.

## Estrategias

- Caching.
- Queue system.
- CDN.
- WebSockets.
- Horizontal scaling.
- Read replicas.

---

# 20. Integraciones Futuras

## Posibles Integraciones

- Seats.io.
- Stripe.
- Meta Ads.
- Google Analytics.
- TikTok Pixel.
- Mailchimp.
- HubSpot.
- CRM.
- BI.

---

# 21. Métricas Críticas del Producto

## KPIs

- Conversion rate.
- Tickets vendidos.
- Asistencia real.
- Tiempo de ingreso.
- Tickets rechazados.
- Tiempo de validación.
- Fraude detectado.
- Eventos activos.
- Revenue.

---

# 22. Roadmap MVP

## Fase 1

- Dashboard.
- Eventos.
- Tickets.
- QR.
- Guardias.
- Pagos QR.
- Validación.

---

## Fase 2

- WhatsApp bot.
- App asistentes.
- Reportes avanzados.
- Analytics.

---

## Fase 3

- IA avanzada.
- Recomendaciones.
- Marketing.
- Loyalty.
- Gamificación.

---

# 23. Requerimientos No Funcionales

## Rendimiento

- Respuesta rápida.
- Escaneo instantáneo.
- Alta disponibilidad.

## Disponibilidad

- 99.9% ideal.

## Escalabilidad

- Horizontal.

## Seguridad

- OWASP.
- Auditoría.

## Usabilidad

- Fácil adopción.
- Baja curva aprendizaje.

---

# 24. Filosofía del Producto

QrTicket no debe sentirse como software administrativo pesado.

Debe sentirse:

- Moderno.
- Rápido.
- Inteligente.
- Profesional.
- Confiable.
- Minimalista.
- Operativo.

La experiencia debe priorizar:

- Velocidad.
- Claridad.
- Baja fricción.
- Tiempo real.
- Escalabilidad.

---

# 25. Diferenciación Estratégica

QrTicket compite mediante:

- Mejor UX.
- Operación offline.
- Automatización.
- Ecosistema WhatsApp.
- Contextualización Bolivia.
- Control de acceso robusto.
- Simplicidad.
- Velocidad.

---

# 26. Contexto Estratégico del Mercado Boliviano

## Características del Mercado

- Predominio de pagos QR.
- Alto uso de WhatsApp.
- Infraestructura variable.
- Eventos organizados por estudiantes.
- Bajo nivel de profesionalización.
- Procesos manuales.

QrTicket debe adaptarse a esta realidad.

---

# 27. Principios Técnicos de Implementación

## Arquitectura

Idealmente modular.

## Backend

Separación clara:

- Auth.
- Events.
- Payments.
- Tickets.
- Access.
- Reports.
- Notifications.

---

# 28. Notificaciones

## Canales

- Email.
- WhatsApp.
- Push.
- SMS futuro.

## Casos

- Compra.
- Pago confirmado.
- Ticket emitido.
- Evento próximo.
- Evento cancelado.
- Acceso validado.

---

# 29. Logs y Auditoría

Todo debe ser auditado.

## Logs

- Login.
- Compras.
- Validaciones.
- Cambios.
- Reembolsos.
- Acciones admin.

---

# 30. Branding y Personalización

Cada organizador podría:

- Personalizar colores.
- Ticket branding.
- Logos.
- Landing.
- Templates.

---

# 31. Sistema de Recintos

## Recintos

- Nombre.
- Ubicación.
- Capacidad.
- Puertas.
- Zonas.
- Layout.

---

# 32. Sistema de Puertas

Las validaciones pueden asociarse a:

- Puertas.
- Sectores.
- Zonas.

Esto permite:

- Analytics.
- Restricciones.
- Flujo.

---

# 33. Experiencia Operativa del Día del Evento

El sistema debe estar optimizado para:

- Alta presión.
- Alta concurrencia.
- Operación rápida.
- Decisiones instantáneas.

La UI del control de acceso debe priorizar:

- Contraste.
- Feedback.
- Velocidad.
- Error prevention.

---

# 34. Consideraciones Futuras

## Potenciales funcionalidades

- Reventa oficial.
- Transferencia tickets.
- Loyalty.
- Membresías.
- Marketplace.
- IA predictiva.
- Pricing dinámico.
- Heatmaps en tiempo real.
- Control biométrico.

---

# 35. Resumen Ejecutivo

QrTicket es una plataforma SaaS moderna para gestión de eventos, venta de entradas y control de acceso diseñada para el contexto boliviano.

Su diferenciación principal radica en:

- UX moderna.
- Operación offline.
- Integración con QR bancario.
- Automatización vía WhatsApp.
- Validación QR robusta.
- Escalabilidad.
- Adaptación a eventos universitarios.

El producto debe construirse como un sistema modular, escalable y preparado para evolucionar desde un MVP universitario hasta una plataforma de ticketing profesional de alcance nacional.

