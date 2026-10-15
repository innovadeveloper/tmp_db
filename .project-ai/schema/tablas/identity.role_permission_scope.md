## identity.role_permission_scope
**Tipo:** tabla
**Proposito:** Almacena los ámbitos (scopes) granulares para los permisos de los roles.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| role_permission_scope_id | bigint | No | nextval('identity.role_permission_scope_role_permission_scope_id_seq'::regclass) | Identificador único del registro. |
| role_permission_id | bigint | No | Ninguna | Identificador del permiso de rol asociado. |
| scope_type_id | smallint | No | Ninguna | Identificador del tipo de ámbito. |
| scope_id | bigint | Sí | Ninguna | Identificador del ámbito específico. |
| company_id | integer | No | Ninguna | Identificador de la empresa a la que pertenece el ámbito. |
| is_active | boolean | Sí | true | Indica si el ámbito está activo. |
| created_at | timestamp with time zone | Sí | now() | Fecha y hora de creación del registro. |

**Clave primaria:** role_permission_scope_id

**Claves foraneas:** 
- role_permission_id -> identity.role_permission(role_permission_id)
- company_id -> shared.company(company_id)
- scope_type_id -> identity.scope_type(scope_type_id)

**Indices y restricciones:** 
- idx_role_perm_scope_entity: Índice en (scope_type_id, scope_id)
- idx_role_perm_scope_rp: Índice en (role_permission_id, is_active)
- idx_role_perm_scope_type: Índice en (scope_type_id, company_id)
- role_permission_scope_company_id_fkey: Restricción de clave foránea entre company_id y shared.company.company_id
- role_permission_scope_role_permission_id_fkey: Restricción de clave foránea entre role_permission_id y identity.role_permission.role_permission_id
- role_permission_scope_scope_type_id_fkey: Restricción de clave foránea entre scope_type_id y identity.scope_type.scope_type_id

**Triggers:** 
- trg_role_permission_scopes_change: Dispara una notificación cuando se inserta, actualiza o elimina un registro.

**Particionado:** Ninguna

**Observaciones:** Ninguna
