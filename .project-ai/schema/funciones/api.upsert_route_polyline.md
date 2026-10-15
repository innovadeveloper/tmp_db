## api.upsert_route_polyline
**Proposito:** Inserta o actualiza una polilínea de ruta en la base de datos, dependiendo si ya existe una polilínea con el mismo `route_id` y `direction`.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.upsert_route_polyline_input | Objeto de entrada que contiene los datos de la polilínea a insertar o actualizar. |

**Retorna:** Un objeto `api.upsert_route_polyline_result` que contiene el resultado de la operación, incluyendo el estado de la polilínea (`INSERTED`, `REPLACED`, `SKIPPED`), detalles de la polilínea, y posibles errores.

**Tablas que lee:** `core_operations.route`, `core_operations.route_polyline`.

**Tablas que modifica (INSERT/UPDATE/DELETE):** `core_operations.route_polyline`.

**Funciones que invoca:** No invoca ninguna función externa.

**Logica paso a paso:**
1. Valida que `route_id` no sea nulo.
2. Valida que la ruta exista y esté activa.
3. Valida que `direction` sea uno de los valores permitidos ('IDA', 'VUELTA').
4. Valida que `coordinates` no sea nulo y sea un array JSON.
5. Valida que el array de coordenadas tenga al menos 2 puntos.
6. Valida que cada punto sea un par `[longitude, latitude]` con valores en el rango correcto.
7. Comprueba si ya existe una polilínea con el mismo `route_id` y `direction`.
8. Si existe, compara los datos de la nueva polilínea con los existentes. Si hay cambios, actualiza la polilínea; si no hay cambios, omite la operación.
9. Si no existe, inserta una nueva polilínea.
10. Devuelve el resultado de la operación, incluyendo el estado de la polilínea y detalles de la polilínea.

**Errores y excepciones:**
- `MISSING_ROUTE_ID`: `route_id` es nulo.
- `ROUTE_NOT_FOUND`: La ruta no existe o está inactiva.
- `INVALID_DIRECTION`: `direction` no es válido.
- `MISSING_COORDINATES`: `coordinates` es nulo.
- `INVALID_COORDINATES_FORMAT`: `coordinates` no es un array JSON.
- `INSUFFICIENT_POINTS`: El array de coordenadas tiene menos de 2 puntos.
- `INVALID_COORDINATE_PAIR`: Un punto no es un par `[longitude, latitude]` válido.
- `COORDINATE_OUT_OF_RANGE`: Un punto tiene valores de longitud o latitud fuera del rango permitido.
- `CONCURRENT_CONFLICT`: Ocurrió un conflicto de concurrencia al intentar insertar la polilínea.
- `INTERNAL_ERROR`: Error interno inesperado.

**Observaciones:** La función utiliza `SECURITY DEFINER` para ejecutar operaciones en el nombre del propietario de la función. No utiliza SQL dinámico.
