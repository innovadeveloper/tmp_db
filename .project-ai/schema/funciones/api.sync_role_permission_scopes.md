## api.sync_role_permission_scopes
**Proposito:** Sincroniza los scopes de permiso asociados a un role_permission_id, insertando, actualizando y desactivando scopes según los datos proporcionados.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.sync_role_permission_scopes_input | Objeto de entrada que contiene el role_permission_id y los scopes a sincronizar. |

**Retorna:** `api.sync_role_permission_scopes_result`, un objeto que contiene el resultado de la operación, incluyendo detalles de cada scope procesado.

**Tablas que lee:** 
- `identity.role_permission`
- `identity.permission`
- `identity.scope_type`
- `shared.company`
- `identity.role_permission_scope`

**Tablas que modifica (INSERT/UPDATE/DELETE):** 
- `identity.role_permission_scope`

**Funciones que invoca:** 
- `COALESCE`
- `EXISTS`
- `IS NOT DISTINCT FROM`
- `ARRAY[]::api.scope_item_result[]`

**Logica paso a paso:** 
1. Valida que `role_permission_id` no sea nulo.
2. Valida que el `role_permission_id` exista y esté activo.
3. Valida que el array de scopes no sea nulo.
4. Para cada scope en el array:
   - Valida que `scope_type_id` y `company_id` no sean nulos.
   - Valida que `scope_type_id` y `company_id` existan en sus respectivas tablas.
   - Valida que no haya duplicados en el batch.
   - Busca si el scope ya existe y actualiza o inserta según sea necesario.
5. Desactiva los scopes activos que no están en el payload.
6. Devuelve el resultado de la operación, incluyendo detalles de cada scope procesado.

**Errores y excepciones:** 
- `MISSING_ROLE_PERMISSION_ID`: `role_permission_id` es obligatorio.
- `ROLE_PERMISSION_NOT_FOUND`: `role_permission_id` no existe o está inactivo.
- `NULL_SCOPES_ARRAY`: El array de scopes es NULL.
- `MISSING_SCOPE_TYPE_ID`: `scope_type_id` es obligatorio en cada ítem.
- `MISSING_COMPANY_ID`: `company_id` es obligatorio en cada ítem.
- `SCOPE_TYPE_NOT_FOUND`: `scope_type_id` no existe en el catálogo.
- `COMPANY_NOT_FOUND`: `company_id` no existe o está inactiva.
- `DUPLICATE_SCOPE_IN_BATCH`: La combinación (scope_type, scope_id, company_id) aparece más de una vez en el lote.
- `INTERNAL_ERROR`: Error interno inesperado.

**Observaciones:** 
- La función utiliza `SECURITY DEFINER` para ejecutar operaciones en el nombre del propietario de la función.
- La función maneja errores y excepciones generales con `WHEN OTHERS THEN`.
