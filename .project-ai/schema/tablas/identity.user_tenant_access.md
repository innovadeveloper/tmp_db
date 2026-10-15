## identity.user_tenant_access
**Tipo:** tabla
**Proposito:** Almacena los permisos de acceso de los usuarios a los tenants.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| user_tenant_access_id | bigint | No | nextval('identity.user_tenant_access_user_tenant_access_id_seq'::regclass) | Identificador único del registro de acceso |
| user_id | bigint | No | Ninguna | Identificador del usuario |
| tenant_id | bigint | No | Ninguna | Identificador del tenant al que el usuario tiene acceso |
| is_active | boolean | Sí | true | Indica si el acceso está activo |
| granted_by | bigint | Sí | Ninguna | Identificador del usuario que concedió el acceso |
| granted_at | timestamp with time zone | Sí | now() | Fecha y hora en que se concedió el acceso |

**Clave primaria:** user_tenant_access_id
**Claves foraneas:** 
- user_id -> identity."user".user_id
- tenant_id -> identity.tenant.tenant_id
- granted_by -> identity."user".user_id (con ON DELETE SET NULL)
**Indices y restricciones:** 
- uq_user_tenant: Único (user_id, tenant_id)
- idx_user_tenant_tenant: B-tree (tenant_id)
- idx_user_tenant_user: B-tree (user_id, is_active)
**Triggers:** 
- trg_user_tenant_access_change: Despacha un evento de cambio de permiso
**Particionado:** Ninguna
**Observaciones:** Ninguna
