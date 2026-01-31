# 🔄 Lógica del Flujo de Aprobación de Solicitudes

Este documento describe el funcionamiento del flujo de Power Automate para la gestión y aprobación de solicitudes registradas desde Microsoft Forms y almacenadas en SharePoint.

---

## 🧩 1. Disparador del flujo

**Trigger:**  
📌 *When a new response is submitted* (Microsoft Forms)

Cuando un usuario envía el formulario, el flujo se activa automáticamente.

Luego se ejecuta:  
➡️ **Get response details** para obtener toda la información ingresada.

---

## 📝 2. Registro de la solicitud en SharePoint

Se crea un nuevo elemento en la lista **Solicitudes** con los datos del formulario:

- Título
- Área
- Tipo de Solicitud
- Monto
- Prioridad
- Fecha de Solicitud
- Detalle
- Correo del solicitante
- Estado = **Nuevo**

---

## ⚖️ 3. Evaluación automática

Se valida si la solicitud necesita aprobación:

**Condición:**
- Si el **Monto > 1000**  
**O**
- Si la **Prioridad = Alta**

👉 Si se cumple → pasa a **aprobación**  
👉 Si no → se **aprueba automáticamente**

---

## 👨‍💼 4. Proceso de aprobación

Acción utilizada:  
📌 **Start and wait for an approval**

Se envía la aprobación al responsable con:

- Datos completos de la solicitud
- Enlace al registro en SharePoint

El flujo se detiene hasta que el aprobador responda.

---

## ✅ 5. Si la solicitud es APROBADA

Se ejecutan las siguientes acciones:

1. Se registra la decisión en la lista **Aprobaciones**
   - ID de Solicitud
   - Aprobador
   - Resultado = Aprobado
   - Comentarios
   - Fecha de decisión

2. Se actualiza la lista **Solicitudes**
   - Estado → **Aprobado**

3. Se crea una tarea en la lista **Tareas Operativas**
   - Responsable
   - Tipo de gestión
   - Estado de tarea → Pendiente

4. Se envía un correo al solicitante indicando que fue aprobada.

---

## ❌ 6. Si la solicitud es RECHAZADA

1. Se guarda el registro en la lista **Aprobaciones**
   - Resultado = Rechazado
   - Comentarios del aprobador

2. Se actualiza la lista **Solicitudes**
   - Estado → **Rechazado**

3. Se notifica por correo al solicitante.

---

## 🔁 7. Resultado final

El flujo permite:

✔ Registrar solicitudes  
✔ Automatizar validaciones  
✔ Gestionar aprobaciones  
✔ Registrar historial de decisiones  
✔ Generar tareas operativas automáticamente  
✔ Notificar a los usuarios
