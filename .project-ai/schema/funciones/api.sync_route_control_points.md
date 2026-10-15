## api.sync_route_control_points
**Proposito:** Sincroniza los puntos de control de una ruta con los proporcionados en el payload. Valida los datos, realiza inserciones, actualizaciones y eliminaciones según sea necesario, y devuelve un resultado detallado.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.sync_route_control_points_input | Objeto de entrada que contiene la ruta y los puntos de control a sincronizar. |

**Retorna:** Un objeto `api.sync_route_control_points_result` que contiene el resultado de la operación, incluyendo detalles de cada punto de control procesado.

**Tablas que lee:** 
- `core_operations.route`
- `core_operations.checkpoint`
- `core_operations.route_control`

**Tablas que modifica (INSERT/UPDATE/DELETE):** 
- `core_operations.route_control`

**Funciones que invoca:** 
- `core_operations.checkpoint%ROWTYPE`
- `core_operations.route_control%ROWTYPE`

**Logica paso a paso:**
1. Valida si la ruta existe y está activa.
2. Valida si el array de puntos de control es NULL o vacío.
3. Procesa cada punto de control:
   - Valida que `checkpoint_id` sea obligatorio y no duplicado.
   - Valida que el `checkpoint_id` exista y pertenezca a la ruta especificada.
   - Valida que el tipo de `checkpoint` sea compatible con el punto de control.
   - Valida los valores de `min_time_minutes`, `max_time_minutes` y `tolerance_minutes`.
4. Realiza inserciones, actualizaciones o eliminaciones según sea necesario.
5. Devuelve un resultado detallado con el estado de cada punto de control procesado.

**Errores y excepciones:** 
- `ROUTE_NOT_FOUND`: La ruta no existe o está inactiva.
- `NULL_POINTS_ARRAY`: El array de puntos de control es NULL. Para eliminar todos los controles, enviar un array vacío.
- `MISSING_CHECKPOINT_ID`: `checkpoint_id` es obligatorio en cada punto de control.
- `DUPLICATE_IN_BATCH`: `checkpoint_id` aparece más de una vez en el mismo lote.
- `CHECKPOINT_NOT_FOUND`: `checkpoint_id` no existe.
- `CHECKPOINT_NOT_IN_ROUTE`: El `checkpoint` no pertenece a la ruta solicitada.
- `TERMINAL_NOT_ALLOWED_AS_CONTROL`: Los `checkpoints` de tipo terminal no pueden configurarse como puntos de control de tiempo.
- `INVALID_MIN_TIME`: `min_time_minutes` debe ser mayor a 0.
- `INVALID_TIME_RANGE`: `max_time_minutes` debe ser >= `min_time_minutes`.
- `INVALID_TOLERANCE`: `tolerance_minutes` no puede ser negativo.
- `INTERNAL_ERROR`: Error interno inesperado.

**Observaciones:** 
- La función utiliza `SECURITY DEFINER` para ejecutar operaciones de base de datos.
- La función maneja transacciones implícitas para asegurar la consistencia de los datos.
