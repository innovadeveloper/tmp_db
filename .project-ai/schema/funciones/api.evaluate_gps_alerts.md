## api.evaluate_gps_alerts
**Proposito:** Evalúa alertas GPS basadas en eventos de movimiento, velocidad y señal GPS, generando o actualizando alertas en la base de datos.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.evaluate_gps_alerts_input | Objeto de entrada que contiene el ID del evento GPS a evaluar. |

**Retorna:** Un objeto `api.evaluate_gps_alerts_result` que contiene el resultado de la evaluación, incluyendo detalles sobre las alertas generadas o actualizadas.

**Tablas que lee:** 
- `fleet.gps_raw_event`: Para obtener el evento GPS.
- `fleet.vehicle`: Para obtener los detalles del vehículo.
- `fleet.vehicle_assignment`: Para obtener el conductor asignado al vehículo.
- `shared.configuration`: Para obtener los umbrales de configuración como velocidad máxima, tiempo detenido y tiempo sin señal.

**Tablas que modifica (INSERT/UPDATE/DELETE):** 
- `core_operations.alert`: Para insertar o actualizar alertas.

**Funciones que invoca:** 
- `jsonb_build_object`: Para construir objetos JSON.

**Logica paso a paso:** 
1. Valida que el `raw_event_id` no sea nulo.
2. Resuelve el evento GPS y el vehículo asociado.
3. Resuelve el conductor activo del vehículo.
4. Lee los umbrales de configuración para velocidad máxima, tiempo detenido y tiempo sin señal.
5. Evalúa la regla de velocidad excesiva (`SPEEDING`):
   - Si la velocidad es mayor que el umbral, genera o actualiza una alerta.
6. Evalúa la regla de detenido fuera de terminal por mucho tiempo (`VEHICLE_STOPPED`):
   - Si el vehículo ha estado detenido durante más tiempo que el umbral, genera o actualiza una alerta.
7. Evalúa la regla de tiempo sin señal GPS (`SIGNAL_LOST`):
   - Si el dispositivo GPS no ha enviado una señal durante más tiempo que el umbral, genera o actualiza una alerta.
8. Devuelve el resultado de la evaluación, incluyendo detalles sobre las alertas generadas o actualizadas.

**Errores y excepciones:** 
- Si el `raw_event_id` es nulo, devuelve un error.
- Si el evento GPS no existe o es demasiado antiguo, devuelve un error.
- Si el `vehicle_id` no existe, devuelve un error.
- Si el `alert_type` no existe o está inactivo, devuelve un error.
- Si ocurre un error interno, devuelve un error con el mensaje de error.

**Observaciones:** 
- La función es segura (`SECURITY DEFINER`).
- Utiliza SQL dinámico para leer los umbrales de configuración.
- La función maneja la creación y actualización de alertas en la tabla `core_operations.alert`.
