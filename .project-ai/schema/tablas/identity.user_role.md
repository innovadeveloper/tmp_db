## identity.user_role
**Tipo:** tabla
**Proposito:** Almacena la asignación de roles a usuarios, incluyendo detalles sobre la activación, asignación y expiración del rol.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| user_role_id | bigint | NO | nextval('identity.user_role_user_role_id_seq'::regclass) | Identificador único de la asignación de rol |
| user_id | bigint | NO | Por confirmar | Identificador del usuario al que se asigna el rol |
| role_id | bigint | NO | Por confirmar | Identificador del rol asignado |
| tenant_id | bigint | NO | Por confirmar | Identificador del inquilino al que pertenece la asignación |
| is_active | boolean | SI | true | Indica si la asignación de rol está activa |
| assigned_by | bigint | SI | Por confirmar | Identificador del usuario que asignó el rol |
| assigned_at | timestamp with time zone | SI | now() | Fecha y hora en que se asignó el rol |
| expires_at | timestamp with time zone | SI | Por confirmar | Fecha y hora en que expira la asignación de rol |

**Clave primaria:** user_role_id

**Claves foraneas:** 
- user_role_assigned_by_fkey -> identity."user".user_id
- user_role_role_id_fkey -> identity.role.role_id
- user_role_tenant_id_fkey -> identity.tenant.tenant_id
- user_role_user_id_fkey -> identity."user".user_id

**Indices y restricciones:** 
- uq_user_role_tenant: Único por user_id, role_id y tenant_id
- idx_user_role_lookup: Índice por user_id, tenant_id, is_active y expires_at (solo para registros activos)
- idx_user_role_role: Índice por role_id
- idx_user_role_user: Índice por user_id, tenant_id y is_active (solo para registros activos)

**Triggers:** 
- trg_user_roles_change: Notifica cambios en las asignaciones de roles a través de un trigger

**Particionado:** Ninguna

**Observaciones:** 
- La columna 'assigned_by' y 'expires_at' pueden tener valores nulos según la definición actual.
- La tabla no tiene restricciones de nulidad explícitas en las columnas 'assigned_by' y 'expires_at', lo que podría permitir valores nulos.
- El índice 'idx_user_role_lookup' está diseñado para mejorar la búsqueda de roles activos por usuario e inquilino, pero solo para registros activos.
