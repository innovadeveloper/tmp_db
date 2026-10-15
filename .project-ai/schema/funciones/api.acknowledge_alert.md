## api.acknowledge_alert
**Proposito:** Esta función permite a un usuario reconocer una alerta, actualizando su estado a "ACKNOWLEDGED" y registrando el evento en el log de actividades.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.acknowledge_alert_input | Un objeto que contiene los detalles de la alerta a reconocer, incluyendo el `alert_id`, `alert_timestamp`, y `acknowledged_by`. |

**Retorna:** Un objeto `api.acknowledge_alert_result` que indica el éxito o fracaso de la operación, incluyendo el estado de la alerta, el usuario que la reconoció, y detalles adicionales.

**Tablas que lee:** 
- `core_operations.alert`
- `core_operations.alert_type`
- `identity."user"`
- `identity.activity_log`

**Tablas que modifica (INSERT/UPDATE/DELETE):** 
- `core_operations.alert` (UPDATE)
- `identity.activity_log` (INSERT)

**Funciones que invoca:** 
- `pg_notify` (comentada)

**Logica paso a paso:**
1. Valida que los campos obligatorios (`alert_id`, `alert_timestamp`, `acknowledged_by`) estén presentes.
2. Valida que el usuario que reconoce la alerta existe y está activo.
3. Busca la alerta por su clave compuesta (`alert_id`, `alert_timestamp`).
4. Valida que la alerta esté en estado "ACTIVE".
5. Si la alerta ya fue reconocida, devuelve una advertencia.
6. Actualiza el estado de la alerta a "ACKNOWLEDGED".
7. Registra el cambio en el log de actividades.
8. Devuelve los detalles de la alerta reconocida.

**Errores y excepciones:** 
- `MISSING_ALERT_KEY`: Si `alert_id` o `alert_timestamp` no están presentes.
- `MISSING_USER`: Si `acknowledged_by` no está presente.
- `USER_NOT_FOUND`: Si el usuario que reconoce la alerta no existe o está inactivo.
- `ALERT_NOT_FOUND`: Si la alerta no existe.
- `ALERT_NOT_ACTIVE`: Si la alerta no está en estado "ACTIVE".
- `INTERNAL_ERROR`: Para cualquier otro error inesperado.

**Observaciones:** 
- La función utiliza `SECURITY DEFINER` para ejecutarse con los privilegios del propietario de la función.
- El registro de cambios se realiza en la tabla `identity.activity_log`.
- La función comenta la invocación a `pg_notify`, lo que significa que no se envían notificaciones en este momento.
