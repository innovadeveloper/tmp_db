## api.update_gps_device_heartbeat
**Proposito:** Actualiza el estado de latido (heartbeat) de un dispositivo GPS, manejando diferentes estados como 'ACTIVE', 'ERROR', 'MAINTENANCE' y 'INACTIVE'. Restaura el estado del vehículo asociado si el dispositivo estaba en 'ERROR'.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.update_gps_device_heartbeat_input | Objeto de entrada que contiene el device_id y el timestamp del latido recibido. |

**Retorna:** api.update_gps_device_heartbeat_result - Un objeto que indica el éxito de la operación, el estado previo y actual del dispositivo, y si el estado del vehículo fue restaurado.

**Tablas que lee:** fleet.gps_device, fleet.vehicle

**Tablas que modifica (INSERT/UPDATE/DELETE):** fleet.gps_device, fleet.vehicle

**Funciones que invoca:** Por confirmar

**Logica paso a paso:**
1. Inicializa las variables de resultado y flags.
2. Valida que el device_id no esté vacío.
3. Busca el dispositivo en la tabla fleet.gps_device.
4. Si el dispositivo no está registrado, establece el flag device_not_registered y retorna.
5. Si el dispositivo está en 'MAINTENANCE', solo actualiza last_communication_at y retorna.
6. Determina el nuevo estado del dispositivo basado en su estado actual.
7. Actualiza el dispositivo en fleet.gps_device con el nuevo estado y last_communication_at.
8. Si el estado cambió de 'ERROR' a 'ACTIVE', intenta restaurar el vehículo asociado.
9. Pobla el objeto de resultado con los datos actualizados.

**Errores y excepciones:** 
- Si ocurre un error, establece el resultado con error_code 'INTERNAL_ERROR' y error_message con el mensaje de error SQL.

**Observaciones:** 
- La función no verifica documentos al restaurar el vehículo, esa responsabilidad es de update_gps_device_status.
- La función es definida con SECURITY DEFINER, lo que permite que cualquier usuario que la invoque tenga los mismos privilegios que el propietario de la función.
