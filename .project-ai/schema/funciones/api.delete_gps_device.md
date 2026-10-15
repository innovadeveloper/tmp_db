## api.delete_gps_device
**Proposito:** Elimina un dispositivo GPS de la base de datos. Recibe un objeto de entrada que puede contener el `gps_device_id` o el `device_id` del dispositivo a eliminar.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.delete_gps_device_input | Objeto de entrada que contiene el `gps_device_id` o el `device_id` del dispositivo a eliminar. |

**Retorna:** Un objeto `api.delete_gps_device_result` que indica el éxito de la operación, el código de error (si existe), el mensaje de error, el `gps_device_id` y `device_id` del dispositivo eliminado, y la fecha y hora de la eliminación.

**Tablas que lee:** `fleet.gps_device`

**Tablas que modifica (INSERT/UPDATE/DELETE):** `fleet.gps_device`

**Funciones que invoca:** N/A

**Logica paso a paso:**
1. Busca el dispositivo en la tabla `fleet.gps_device` utilizando el `gps_device_id` o `device_id` proporcionados en el parámetro de entrada.
2. Si el dispositivo no se encuentra, devuelve un resultado con `success` como `FALSE`, `error_code` como `NOT_FOUND`, y `error_message` como 'GPS device no encontrado'.
3. Si el dispositivo se encuentra, intenta eliminarlo de la tabla `fleet.gps_device`.
4. Devuelve un resultado con `success` como `TRUE`, el `gps_device_id` y `device_id` del dispositivo eliminado, y la fecha y hora de la eliminación.
5. En caso de cualquier error durante la operación, devuelve un resultado con `success` como `FALSE`, `error_code` como `INTERNAL_ERROR`, y `error_message` como el mensaje de error generado por la excepción.

**Errores y excepciones:** 
- `NOT_FOUND`: Se lanza cuando el dispositivo no se encuentra en la base de datos.
- `INTERNAL_ERROR`: Se lanza cuando ocurre un error interno durante la ejecución de la función.

**Observaciones:** La función no incluye validaciones adicionales, como verificar si el dispositivo está asociado a un vehículo. Esto debe ser considerado en una versión futura de la función.
