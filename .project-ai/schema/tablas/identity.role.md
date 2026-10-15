## identity.role
**Tipo:** tabla
**Proposito:** Almacena los roles definidos por cada tenant.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| role_id | bigint | No | nextval('identity.role_role_id_seq'::regclass) | Identificador único del role. |
| tenant_id | bigint | No | Ninguna | Identificador del tenant al que pertenece el role. |
| name | character varying(100) | No | Ninguna | Nombre del role. |
| description | text | Sí | Ninguna | Descripción opcional del role. |
| is_active | boolean | Sí | true | Indica si el role está activo. |
| created_by | bigint | Sí | Ninguna | Identificador del usuario que creó el role. |
| created_at | timestamp with time zone | Sí | now() | Fecha y hora de creación del role. |
| updated_at | timestamp with time zone | Sí | now() | Fecha y hora de la última actualización del role. |

**Clave primaria:** role_id
**Claves foraneas:** created_by -> identity."user"(user_id), tenant_id -> identity.tenant(tenant_id)
**Indices y restricciones:** uq_tenant_role_name (UNIQUE), idx_role_tenant (B-Tree)
**Triggers:** trg_roles_change (AFTER UPDATE OF is_active)
**Particionado:** Ninguna
**Observaciones:** Ninguna
