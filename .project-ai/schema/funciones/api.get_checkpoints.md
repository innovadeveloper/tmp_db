## api.get_checkpoints
**Proposito:** Obtiene los puntos de control (checkpoints) asociados a una ruta específica, aplicando filtros opcionales para dirección y tipos de puntos de control.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.get_checkpoints_input | Objeto de entrada que contiene los parámetros de la consulta, incluyendo `route_id`, `direction` y `checkpoint_types`. |

**Retorna:** Un objeto `api.get_checkpoints_result` que contiene los resultados de la consulta, incluyendo la lista de puntos de control, detalles de la ruta y filtros aplicados.

**Tablas que lee:** 
- `core_operations.route`: Para obtener información sobre la ruta especificada.
- `core_operations.checkpoint`: Para obtener los puntos de control asociados a la ruta.

**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla.

**Funciones que invoca:** No invoca ninguna función externa.

**Logica paso a paso:**
1. Valida que `route_id` no sea nulo.
2. Valida que la ruta exista y esté activa.
3. Normaliza y valida el parámetro `direction` si se proporciona.
4. Normaliza y valida el parámetro `checkpoint_types` si se proporciona.
5. Realiza una consulta para obtener los puntos de control que cumplen con los filtros aplicados.
6. Pobla el objeto de resultado con los datos obtenidos y los filtros aplicados.

**Errores y excepciones:**
- `MISSING_ROUTE_ID`: Si `route_id` es nulo.
- `ROUTE_NOT_FOUND`: Si la ruta no existe o está inactiva.
- `INVALID_DIRECTION`: Si la dirección proporcionada no es válida.
- `DIRECTION_ROUTE_TYPE_MISMATCH`: Si la dirección proporcionada no es compatible con el tipo de ruta.
- `INVALID_CHECKPOINT_TYPE`: Si algún tipo de punto de control proporcionado no es válido.
- `INTERNAL_ERROR`: Para cualquier otro error inesperado.

**Observaciones:** La función utiliza `SECURITY DEFINER` para permitir que los usuarios con privilegios ejecuten la función, aunque no realiza operaciones que requieran privilegios adicionales. No utiliza SQL dinámico.
