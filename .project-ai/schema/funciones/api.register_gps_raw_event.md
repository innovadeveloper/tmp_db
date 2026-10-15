## api.register_gps_raw_event
**Proposito:** Registra un evento de GPS crudo en la base de datos. Resuelve el `gps_device_id` y `vehicle_id` si no se proporcionan, valida las coordenadas y registra el evento en la tabla `fleet.gps_raw_event`.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.register_gps_raw_event_input | Objeto de entrada que contiene los datos del evento GPS crudo a registrar. |

**Retorna:** Un objeto `api.register_gps_raw_event_result` que indica el éxito o fracaso del registro, el ID del evento registrado, el ID del dispositivo GPS, la marca de tiempo del evento y la hora de creación.

**Tablas que lee:** `fleet.gps_device`

**Tablas que modifica (INSERT/UPDATE/DELETE):** `fleet.gps_raw_event`

**Funciones que invoca:** `utilities.create_gps_partition`

**Logica paso a paso:**
1. Resuelve el `gps_device_id` si no se proporciona en el `p_input`.
2. Resuelve el `vehicle_id` si no se proporciona en el `p_input`.
3. Valida las coordenadas de latitud y longitud.
4. Crea una partición para el evento GPS si no existe.
5. Inserta el evento en la tabla `fleet.gps_raw_event`.
6. Devuelve el resultado del registro.

**Errores y excepciones:**
- `NO_DEVICE_FOUND`: No se encontró ningún dispositivo GPS en la base de datos.
- `INVALID_LATITUDE`: La latitud proporcionada no es válida.
- `INVALID_LONGITUDE`: La longitud proporcionada no es válida.
- `INTERNAL_ERROR`: Error interno inesperado.

**Observaciones:** La función utiliza `SECURITY DEFINER` para ejecutar operaciones en el esquema `utilities`. No se utiliza SQL dinámico.
