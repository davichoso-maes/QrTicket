# Prompt para desarrollar QrTicket en Replit

## Instrucciones

Crea un sistema web MVP llamado **QrTicket**.

---

## Objetivo
Desarrollar una plataforma para gestión de eventos universitarios, venta de entradas con QR y control de acceso.

---

## Stack
- Next.js con App Router
- TypeScript
- Tailwind CSS
- PostgreSQL
- Prisma ORM
- Auth con email y contraseña
- Diseño responsive moderno tipo SaaS

---

## Roles
- Superadmin
- Organizador
- Guardia
- Asistente

---

## Módulos del sistema

### 1. Login
- Pantalla de inicio de sesión
- Validación de usuario
- Redirección según rol

### 2. Dashboard principal
- KPIs: eventos activos, tickets vendidos, ingresos, asistentes
- Cards de eventos activos
- Botón “Crear evento”

### 3. Gestión de eventos
- Crear evento
- Editar evento
- Listar eventos
- Estados: borrador, activo, agotado, finalizado
- Campos:
  - título
  - descripción
  - fecha
  - ubicación
  - capacidad
  - imagen/banner
  - organizador

### 4. Configuración de tickets
- Tipos de entrada: General, VIP, Estudiante, etc.
- Precio
- Cupo
- Cantidad disponible
- Generación de ticket QR único

### 5. Pagos
- Registrar pagos por QR
- Estado: pendiente, confirmado, rechazado
- Método de pago: QR, Libélula, BNB, Visa, Unión
- Relacionar pago con usuario y ticket

### 6. Asistentes
- Lista de asistentes por evento
- Ticket asociado
- Estado de ingreso
- Hora de ingreso
- Guardia que validó

### 7. Guardias
- Crear guardias
- Asignar guardias a eventos
- Credenciales para app/control de ingreso

### 8. Control de ingreso
- Pantalla simple para guardias
- Input o simulador para escanear QR
- Validar ticket
- Mostrar resultado:
  - Acceso permitido
  - Ticket ya usado
  - Ticket inválido
  - Evento incorrecto

### 9. Reportes por evento
- Tickets vendidos
- Tickets usados
- Tickets no usados
- Ingresos totales
- Asistencia porcentual

---

## Base de datos

Crear modelos Prisma para:
- User
- Event
- TicketType
- Ticket
- Payment
- GuardAssignment
- AccessLog

---

## Requisitos
- Código limpio y modular
- UI en español
- Datos de ejemplo contextualizados a Bolivia y eventos universitarios
- Seed inicial con usuarios, eventos y tickets
- README con instrucciones para correr el proyecto
- Usar buenas prácticas de seguridad básicas
- Preparar el proyecto para escalar luego con app móvil y WhatsApp Bot

---

## Nota importante

Empieza solo con el MVP web.  
No desarrolles todavía la app móvil ni WhatsApp Bot; solo deja la arquitectura preparada.
