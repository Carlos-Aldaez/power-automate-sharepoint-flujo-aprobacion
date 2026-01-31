# Lista: Tareas Operativas

Esta lista contiene las tareas generadas cuando una solicitud es aprobada.  
Representa el trabajo que debe ejecutar el área operativa.

## Columnas

| Columna        | Tipo de dato        | Descripción |
|----------------|---------------------|-------------|
| Title          | Texto               | Nombre de la tarea |
| SolicitudID    | Número              | ID de la solicitud relacionada |
| Responsable    | Persona o Grupo     | Persona encargada de ejecutar la tarea |
| EstadoTarea    | Opción              | Pendiente, En proceso, Finalizada |
| FechaInicio    | Fecha y hora        | Fecha en que se creó la tarea |
| FechaFin       | Fecha y hora        | Fecha en que se completó la tarea |
| Observaciones  | Múltiples líneas    | Comentarios sobre la ejecución |

## Uso en el flujo

- Se crea automáticamente cuando una solicitud es aprobada.
- Inicia en estado **Pendiente**.
- Puede ser actualizada manualmente por el responsable o por un segundo flujo.
