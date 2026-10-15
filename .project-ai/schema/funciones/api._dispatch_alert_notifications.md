## api._dispatch_alert_notifications
**Proposito:** Esta función se encarga de encolar las notificaciones de alerta para los destinatarios configurados en el sistema. Recibe detalles de la alerta y determina a quién debe enviar la notificación, luego inserta registros en la tabla `alert_communication_log` para cada canal de notificación configurado.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_alert_id | bigint | Identificador único de la alerta. |
| p_alert_type_id | integer | Identificador del tipo de alerta. |
| p_entity_type | character varying | Tipo de entidad relacionada con la alerta (DRIVER, VEHICLE, TRIP, ROUTE, SYSTEM). |
| p_entity_id | bigint | Identificador de la entidad relacionada con la alerta. |
| p_vehicle_id | integer | Identificador del vehículo asociado a la alerta. |
| p_driver_id | integer | Identificador del conductor asociado a la alerta. |

**Retorna:** Entero que indica el número de notificaciones encoladas.

**Tablas que lee:** 
- `core_operations.alert_type`: Para obtener los canales de notificación asociados al tipo de alerta.

**Tablas que modifica (INSERT/UPDATE/DELETE):** 
- `core_operations.alert_communication_log`: Para insertar registros de notificación encolada.

**Funciones que invoca:** 
- `pg_notify`: Para enviar una notificación a través de un canal de notificación.

**Logica paso a paso:**
1. Lee los canales de notificación configurados para el tipo de alerta.
2. Determina el receptor principal según el tipo de entidad.
3. Inserta un registro en `alert_communication_log` para cada canal de notificación configurado.
4. Envía una notificación a través del canal `alert_new`.

**Errores y excepciones:** 
- No hay validaciones explícitas en el código proporcionado.

**Observaciones:** 
- La función utiliza `pg_notify` para enviar una notificación, lo que implica que debe haber un listener configurado para recibir estas notificaciones.
- La función no maneja errores específicos, lo que podría llevar a que las notificaciones no se encolen correctamente si ocurren errores en el proceso de inserción en `alert_communication_log`.
