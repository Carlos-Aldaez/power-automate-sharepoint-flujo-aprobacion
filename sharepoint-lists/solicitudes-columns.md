# Lista: Solicitudes

Esta lista almacena todas las solicitudes enviadas por los usuarios desde Microsoft Forms.  
Es el punto de inicio del flujo de aprobaciones.

## Columnas

| Columna          | Tipo de dato        | Descripción |
|------------------|---------------------|-------------|
| Title            | Texto               | Título o asunto de la solicitud |
| Área             | Opción              | Área solicitante (Ej: TI, Finanzas, RRHH) |
| TipoSolicitud    | Opción              | Tipo de requerimiento solicitado |
| Monto            | Moneda / Número     | Monto asociado a la solicitud |
| Prioridad        | Opción              | Baja, Media, Alta |
| Estado           | Opción              | Nuevo, En revisión, Aprobado, Rechazado, Finalizado |
| FechaSolicitud   | Fecha y hora        | Fecha requerida de solicitud |
| Detalle          | Múltiples líneas    | Descripción detallada de la solicitud |
|

## Uso en el flujo

- Se crea un registro automáticamente al recibir una respuesta de Forms.
- El flujo actualiza el **Estado** según la etapa de aprobación.
- Se usa como referencia para crear registros en las listas **Aprobaciones** y **Tareas Operativas**.
