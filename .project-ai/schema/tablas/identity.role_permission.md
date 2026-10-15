## identity.role_permission
**Tipo:** tabla
**Proposito:** Almacena los permisos asignados a los roles en el sistema.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| role_permission_id | bigint | No | nextval('identity.role_permission_role_permission_id_seq'::regclass) | Identificador único de la asignación de permiso a rol. |
| role_id | bigint | No | Ninguna | Identificador del rol al que se asigna el permiso. |
| permission_id | integer | No | Ninguna | Identificador del permiso asignado al rol. |
| is_active | boolean | No | true | Indica si el permiso está activo. |
| created_at | timestamp with time zone | No | now() | Fecha y hora en que se creó la asignación de permiso. |

**Clave primaria:** role_permission_id
**Claves foraneas:** 
- role_id -> identity.role.role_id
- permission_id -> identity.permission.permission_id
**Indices y restricciones:** 
- uq_role_permission: Único para asegurar que no haya dos asignaciones de permiso para el mismo rol y permiso.
- idx_role_perm_permission: Índice en permission_id para mejorar la eficiencia de las consultas.
- idx_role_perm_role: Índice en role_id y is_active para mejorar la eficiencia de las consultas filtradas por rol y estado de actividad.
**Triggers:** 
- trg_role_permissions_change: Lanza un evento de notificación cuando se inserta, actualiza o elimina una asignación de permiso.
**Particionado:** Ninguna
**Observaciones:** Ninguna
