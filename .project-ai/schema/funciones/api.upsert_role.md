## api.upsert_role
**Proposito:** Inserta o actualiza un rol en la base de datos, dependiendo de si se proporciona un `role_id` o no. Si el `role_id` es `NULL`, se realiza una inserción. Si el `role_id` no es `NULL`, se realiza una actualización.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.upsert_role_input | Objeto de entrada que contiene los datos del rol a insertar o actualizar. |

**Retorna:** Un objeto `api.upsert_role_result` que contiene el resultado de la operación, incluyendo el `role_id`, el estado de la operación (`INSERTED`, `UPDATED`, `SKIPPED`), detalles del rol, y posibles errores.

**Tablas que lee:** `identity.tenant`, `identity.role`, `identity.permission_template`, `identity.permission_template_detail`, `identity.permission`, `identity.role_permission`.

**Tablas que modifica (INSERT/UPDATE/DELETE):** `identity.role`, `identity.role_permission`.

**Funciones que invoca:** No invoca ninguna función externa.

**Logica paso a paso:**
1. Si `role_id` es `NULL`, valida los parámetros de entrada (`tenant_id`, `name`, etc.) y realiza la inserción del rol.
2. Si `role_id` no es `NULL`, valida que el rol exista y realiza la actualización del rol si hay cambios.
3. Si se proporciona `clone_template_id`, clona los permisos del template al crear el rol o al actualizarlo.
4. Maneja excepciones como conflictos de unicidad y errores internos.

**Errores y excepciones:** 
- `MISSING_TENANT_ID`: El `tenant_id` es obligatorio al crear un rol.
- `TENANT_NOT_FOUND`: El `tenant_id` no existe o está inactivo.
- `MISSING_ROLE_NAME`: El `name` es obligatorio al crear o actualizar un rol.
- `DUPLICATE_ROLE_NAME`: El nombre del rol ya existe en el tenant.
- `CREATOR_NOT_FOUND`: El `created_by` especificado no existe.
- `TEMPLATE_NOT_FOUND`: El `permission_template_id` especificado no existe.
- `TEMPLATE_INACTIVE`: El template especificado está inactivo.
- `INTERNAL_ERROR`: Error interno inesperado.

**Observaciones:** La función utiliza `SECURITY DEFINER` para ejecutar operaciones como `INSERT` y `UPDATE` en las tablas `identity.role` y `identity.role_permission`. No utiliza SQL dinámico.
