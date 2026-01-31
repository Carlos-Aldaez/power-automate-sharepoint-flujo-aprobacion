# ⚙️ Guía Completa de Configuración  
## Sistema de Gestión y Aprobación de Solicitudes  
Power Automate + Microsoft Forms + SharePoint

Este documento explica paso a paso cómo construir el sistema completo de registro, aprobación y gestión de solicitudes.

---

## 🧱 1. Crear las Listas en SharePoint

Crea un sitio en SharePoint (por ejemplo: **Gestión de Solicitudes**) y dentro del sitio crea las siguientes listas.

---

### 📌 Lista 1: **Solicitudes**

Aquí se almacenan todas las solicitudes enviadas por los usuarios.

| Columna | Tipo de dato | Descripción |
|--------|--------------|-------------|
| Title | Texto (una línea) | Título o nombre de la solicitud |
| Área | Opción | Área del solicitante |
| TipoSolicitud | Opción | Tipo de requerimiento |
| Monto | Moneda o Número | Monto solicitado |
| Prioridad | Opción (Alta, Media, Baja) | Nivel de urgencia |
| Estado | Opción (Nuevo, En revisión, Aprobado, Rechazado) | Estado del proceso |
| FechaSolicitud | Fecha y hora | Fecha en que se envió el formulario |
| Detalle | Texto largo | Descripción del requerimiento |

---

### 📌 Lista 2: **Aprobaciones**

Guarda el historial de decisiones de los aprobadores.

| Columna | Tipo de dato | Descripción |
|--------|--------------|-------------|
| Title | Texto | Título de la solicitud |
| SolicitudID | Número | ID de la solicitud en la lista Solicitudes |
| Aprobador | Persona o Grupo | Usuario que aprobó o rechazó |
| Resultado | Opción (Aprobado, Rechazado) | Resultado de la evaluación |
| Comentarios | Texto largo | Comentarios del aprobador |
| FechaDecision | Fecha y hora | Momento de la decisión |

---

### 📌 Lista 3: **Tareas Operativas**

Se generan automáticamente cuando una solicitud es aprobada.

| Columna | Tipo de dato | Descripción |
|--------|--------------|-------------|
| Title | Texto | Nombre de la tarea |
| Responsable | Persona o Grupo | Persona encargada de ejecutarla |
| TipoGestion | Texto | Tipo de acción a realizar |
| EstadoTarea | Opción (Pendiente, En proceso, Finalizada) | Estado de la tarea |
| RelacionSolicitud | Número | ID de la solicitud relacionada |

---

## 📝 2. Crear el Formulario en Microsoft Forms

Crea un formulario con preguntas como:

- Título de la solicitud  
- Área  
- Tipo de solicitud  
- Monto  
- Prioridad  
- Detalle de la solicitud  

Este formulario será el punto de entrada de la información.

---

## 🔄 3. Crear el Flujo en Power Automate

1. Ir a **Power Automate**
2. Clic en **Crear**
3. Elegir **Flujo automatizado**
4. Nombre sugerido: `Gestión de Solicitudes`
5. Disparador:  
   **When a new response is submitted (Microsoft Forms)**

---

## 🔍 4. Obtener los detalles del formulario

Agregar acción:  
**Get response details**

Seleccionar el mismo formulario para recuperar todas las respuestas.

---

## 📥 5. Registrar la solicitud en SharePoint

Agregar acción: **Create item**

Lista: **Solicitudes**

Mapear todos los campos del formulario a las columnas de la lista.

Configurar:
- **Estado = Nuevo**
- **FechaSolicitud = Fecha de envío**
- **Correo = correo del usuario**

---

## ⚖️ 6. Evaluación automática

Agregar una **Condición**:

Monto > 1000
OR
Prioridad = Alta


### Si NO cumple la condición  
➡️ Actualizar Estado = **Aprobado** (se aprueba automáticamente)

### Si SÍ cumple la condición  
➡️ Continuar al proceso de aprobación

---

## 👨‍💼 7. Enviar solicitud de aprobación

Agregar acción:  
**Start and wait for an approval**

Configurar:
- Tipo: **Aprobación básica**
- Asignado a: correo del aprobador
- Título: “Aprobación de solicitud ID”
- Detalles: incluir datos de la solicitud
- Link: enlace al elemento de SharePoint

El flujo se detiene hasta que el aprobador responda.

---

## ✅ 8. Si la solicitud es APROBADA

1. **Crear registro en lista Aprobaciones**
   - Resultado = Aprobado
   - Guardar comentarios y aprobador

2. **Actualizar lista Solicitudes**
   - Estado → Aprobado

3. **Crear tarea en Tareas Operativas**
   - Responsable
   - Tipo de gestión
   - EstadoTarea = Pendiente

4. **Enviar correo al solicitante**
   - Informando que su solicitud fue aprobada

---

## ❌ 9. Si la solicitud es RECHAZADA

1. Registrar decisión en **Aprobaciones**
2. Actualizar **Solicitudes → Estado = Rechazado**
3. Enviar correo notificando el rechazo

---

## 📊 10. Crear vistas para seguimiento

En la lista **Solicitudes** crear vistas personalizadas:

- **Mis solicitudes** → Creado por = [Yo]  
- **Pendientes de aprobación** → Estado = En revisión  
- **Aprobadas** → Estado = Aprobado  
- **Rechazadas** → Estado = Rechazado  

---

## 🎯 Resultado Final

Con esta configuración tendrás un sistema que permite:

✔ Registrar solicitudes automáticamente  
✔ Evaluar reglas de negocio  
✔ Gestionar aprobaciones  
✔ Guardar historial de decisiones  
✔ Generar tareas operativas  
✔ Notificar a los usuarios por correo  
✔ Hacer seguimiento desde SharePoint  

---
