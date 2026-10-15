## api.upsert_route
**Proposito:** Inserta o actualiza una ruta en la base de datos, dependiendo si el `route_id` proporcionado es `NULL` o no. Realiza validaciones y control de errores para garantizar la integridad de los datos.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.upsert_route_input | Objeto de entrada que contiene los datos de la ruta a insertar o actualizar. |

**Retorna:** Un objeto `api.upsert_route_result` que contiene el resultado de la operación, incluyendo el estado de éxito, cualquier error que ocurra, y los detalles de la ruta resultante.

**Tablas que lee:** 
- `core_operations.route`: Para verificar la existencia de una ruta y obtener sus detalles.
- `shared.company`: Para verificar la existencia y estado de la empresa asociada a la ruta.

**Tablas que modifica (INSERT/UPDATE/DELETE):** 
- `core_operations.route`: Para insertar o actualizar una ruta.

**Funciones que invoca:** 
- `NULL`: No invoca ninguna función externa.

**Logica paso a paso:** 
1. Si `route_id` es `NULL`, verifica que los campos obligatorios (`company_id`, `code`, `name`) estén presentes y válidos.
2. Si `route_id` no es `NULL`, verifica que la ruta exista y que los campos proporcionados sean válidos.
3. Compara los valores proporcionados con los existentes para detectar cambios.
4. Si hay cambios, actualiza la ruta en la base de datos.
5. Si no hay cambios, marca la operación como `SKIPPED`.
6. Si `route_id` es `NULL`, inserta una nueva ruta en la base de datos.
7. Llena el objeto de resultado con los detalles de la ruta final, incluyendo su estado (`INSERTED`, `UPDATED`, `SKIPPED`), cualquier campo incompleto y cualquier error que ocurra.

**Errores y excepciones:** 
- `unique_violation`: Si ocurre un conflicto de unicidad debido a una violación de la restricción única en la columna `code` de la tabla `core_operations.route`.
- `OTHERS`: Para cualquier otro error inesperado, capturado y manejado con un mensaje de error interno.

**Observaciones:** 
- La función utiliza `COALESCE` y `NULLIF` para manejar valores nulos y evitar problemas de actualización.
- La función verifica la existencia de la empresa y su estado activo antes de crear una nueva ruta.
- La función maneja la validación de campos obligatorios y únicos.
- La función utiliza `NOW()` para establecer la fecha y hora de actualización.
- La función captura y maneja excepciones para errores de integridad y errores internos.
