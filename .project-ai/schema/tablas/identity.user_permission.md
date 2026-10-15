## identity.user_permission
**Tipo:** tabla
**Proposito:** Almacena los permisos granulares asignados a los usuarios en diferentes empresas.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| user_permission_id | bigint | No | nextval('identity.user_permission_user_permission_id_seq'::regclass) | Identificador único de la asignación de permiso |
| user_id | bigint | No | Ninguna | Identificador del usuario al que se asigna el permiso |
| company_id | integer | No | Ninguna | Identificador de la empresa a la que se asigna el permiso |
| permission_id | integer | No | Ninguna | Identificador del permiso asignado |
| granted_by | bigint | Sí | Ninguna | Identificador del usuario que otorgó el permiso |
| granted_at | timestamp with time zone | Sí | now() | Fecha y hora en que se otorgó el permiso |
| expires_at | timestamp with time zone | Sí | Ninguna | Fecha y hora en que expira el permiso |
| is_active | boolean | Sí | true | Indica si el permiso está activo |

**Clave primaria:** user_permission_id
**Claves foraneas:** 
- user_id -> identity."user".user_id
- company_id -> shared.company.company_id
- permission_id -> identity.permission.permission_id
- granted_by -> identity."user".user_id (nullable)

**Indices y restricciones:** 
- uq_user_company_permission: Único por user_id, company_id y permission_id
- idx_user_perm_expires: Índice por expires_at para permisos con fecha de expiración activa
- idx_user_perm_full_check: Índice compuesto por user_id, company_id, permission_id, is_active y expires_at
- idx_user_perm_permission: Índice por permission_id
- idx_user_perm_user_company: Índice por user_id, company_id y is_active

**Triggers:** No se especifican en el SQL proporcionado

**Particionado:** No se especifica en el SQL proporcionado

**Observaciones:** Ninguna
