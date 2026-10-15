## api.create_alert
**Proposito:** Crea una nueva alerta en el sistema, validando los parámetros de entrada y asegurándose de que los tipos de alerta y entidades sean válidos.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.create_alert_input | Objeto de entrada que contiene los detalles de la alerta a crear. |

**Retorna:** Un objeto `api.create_alert_result` que indica el éxito o fracaso de la operación, incluyendo detalles sobre la alerta creada y cualquier error que ocurra.

**Tablas que lee:** 
- `core_operations.alert_type`: Para validar el tipo de alerta.
- `fleet.vehicle`: Para validar el `vehicle_id` cuando `entity_type` es 'VEHICLE'.
- `hr.driver`: Para validar el `driver_id` cuando `entity_type` es 'DRIVER'.

**Tablas que modifica (INSERT/UPDATE/DELETE):** 
- `core_operations.alert`: Para insertar la nueva alerta.

**Funciones que invoca:** 
- `api._dispatch_alert_notifications`: Para encolar las notificaciones asociadas a la alerta.

**Logica paso a paso:** 
1. Valida que `alert_type_id` no sea nulo.
2. Valida que el `alert_type_id` exista y esté activo.
3. Valida que `entity_type` sea uno de los valores permitidos.
4. Valida que `entity_id` no sea nulo.
5. Valida que `entity_type` y `entity_id` sean coherentes (por ejemplo, `entity_type` 'VEHICLE' requiere `vehicle_id`).
6. Valida que las coordenadas `latitude` y `longitude` sean coherentes si se proporcionan.
7. Resuelve el timestamp de la alerta.
8. Calcula el `auto_closed_at` si el tipo de alerta tiene `auto_close_after_min`.
9. Inserta la nueva alerta en la tabla `core_operations.alert`.
10. Encola las notificaciones asociadas a la alerta.
11. Pobla el objeto de resultado con los detalles de la alerta creada.

**Errores y excepciones:** 
- `MISSING_ALERT_TYPE_ID`: Si `alert_type_id` es nulo.
- `ALERT_TYPE_NOT_FOUND`: Si el `alert_type_id` no existe.
- `ALERT_TYPE_INACTIVE`: Si el tipo de alerta está inactivo.
- `INVALID_ENTITY_TYPE`: Si `entity_type` no es uno de los valores permitidos.
- `MISSING_ENTITY_ID`: Si `entity_id` es nulo.
- `ENTITY_TYPE_VEHICLE_REQUIRES_VEHICLE_ID`: Si `entity_type` es 'VEHICLE' y `vehicle_id` es nulo.
- `VEHICLE_NOT_FOUND`: Si `vehicle_id` no existe.
- `ENTITY_TYPE_DRIVER_REQUIRES_DRIVER_ID`: Si `entity_type` es 'DRIVER' y `driver_id` es nulo.
- `DRIVER_NOT_FOUND`: Si `driver_id` no existe.
- `ENTITY_TYPE_TRIP_REQUIRES_TRIP_ID`: Si `entity_type` es 'TRIP' y `trip_id` es nulo.
- `INCOMPLETE_COORDINATES`: Si se proporcionan solo `latitude` o `longitude`.
- `INVALID_LATITUDE`: Si `latitude` está fuera del rango [-90, 90].
- `INVALID_LONGITUDE`: Si `longitude` está fuera del rango [-180, 180].
- `INTERNAL_ERROR`: Para cualquier otro error inesperado.

**Observaciones:** 
- La función utiliza `SECURITY DEFINER` para ejecutar con los privilegios del propietario de la función.
- La función maneja errores y excepciones generales, devolviendo un objeto de resultado con el código de error y el mensaje correspondiente.
