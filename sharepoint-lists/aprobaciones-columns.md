# Lista: Aprobaciones

Esta lista registra cada decisión tomada sobre una solicitud.  
Funciona como historial de auditoría del proceso de aprobación.

## Columnas

| Columna        | Tipo de dato        | Descripción |
|----------------|---------------------|-------------|
| Title          | Texto               | Título de la solicitud relacionada |
| SolicitudID    | Número              | ID de la solicitud en la lista Solicitudes |
| Aprobador      | Persona o Grupo     | Usuario que realizó la aprobación o rechazo |
| Resultado      | Opción              | Aprobado / Rechazado / Aprobado automático |
| Comentarios    | Múltiples líneas    | Comentarios del aprobador |
| FechaDecision  | Fecha y hora        | Fecha en que se tomó la decisión |

## Uso en el flujo

- Se crea un registro cada vez que un aprobador responde.
- Guarda los comentarios enviados desde Power Automate.
- Permite auditoría y seguimiento del proceso.
