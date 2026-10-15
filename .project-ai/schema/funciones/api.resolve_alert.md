## api.resolve_alert
**Proposito:** Resuelve una alerta en el sistema, actualizando su estado a "RESOLVED" y registrando el cambio en el log de actividades.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.resolve_alert_input | Objeto de entrada que contiene los detalles de la alerta a resolver, incluyendo el ID de la alerta, el timestamp, el usuario que la resuelve y las notas de resolución. |

**Retorna:** Un objeto `api.resolve_alert_result` que indica el éxito o fracaso de la operación, junto con detalles sobre la alerta resuelta y cualquier advertencia o error relevante.

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
1. Valida que los campos obligatorios (`alert_id`, `alert_timestamp`, `resolved_by`) estén presentes.
2. Verifica que el usuario que resuelve la alerta existe y está activo.
3. Busca la alerta en la base de datos.
4. Verifica si la alerta ya está cerrada o cerrada automáticamente, en cuyo caso devuelve una advertencia.
5. Valida que la alerta esté en un estado válido para ser resuelta (`ACTIVE` o `ACKNOWLEDGED`).
6. Si el tipo de alerta requiere reconocimiento y la alerta está activa sin reconocimiento, devuelve un error.
7. Calcula los tiempos de respuesta (tiempo para reconocimiento y tiempo para resolución).
8. Actualiza el estado de la alerta a "RESOLVIDO" y registra la resolución en la base de datos.
9. Registra el cambio en el log de actividades.
10. Devuelve los detalles de la alerta resuelta y los tiempos de respuesta.

**Errores y excepciones:** 
- `MISSING_ALERT_KEY`: Si `alert_id` o `alert_timestamp` no están presentes.
- `MISSING_USER`: Si `resolved_by` no está presente.
- `USER_NOT_FOUND`: Si el usuario que resuelve la alerta no existe o está inactivo.
- `ALERT_NOT_FOUND`: Si la alerta no existe.
- `ALERT_INVALID_STATUS`: Si la alerta no está en un estado válido para ser resuelta.
- `ACKNOWLEDGMENT_REQUIRED`: Si el tipo de alerta requiere reconocimiento y la alerta está activa sin reconocimiento.
- `INTERNAL_ERROR`: Cualquier otro error inesperado.

**Observaciones:** 
- La función verifica el estado de la alerta y devuelve advertencias en lugar de errores para casos especiales como alertas ya cerradas o cerradas automáticamente.
- La función registra el cambio en el log de actividades, lo que permite un seguimiento de todas las operaciones realizadas.
- La función utiliza una transacción implícita para asegurar que todos los cambios se realicen correctamente o ninguno en caso de error.
