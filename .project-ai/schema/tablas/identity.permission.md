## identity.permission
**Tipo:** tabla
**Proposito:** Almacena los permisos disponibles en el sistema, asociados a módulos, recursos y acciones específicas.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| permission_id | integer | No | nextval('identity.permission_permission_id_seq'::regclass) | Identificador único del permiso |
| code | character varying(100) | No | | Código único del permiso, formato: module.resource.action (ej: logistics.route.view) |
| description | text | Sí | | Descripción detallada del permiso |
| module | character varying(50) | No | | Módulo del sistema al que pertenece el permiso (logistics, finance, hr, fleet) |
| is_active | boolean | Sí | true | Indica si el permiso está activo |
| created_at | timestamp with time zone | Sí | now() | Fecha y hora de creación del permiso |
| resource | character varying(50) | Sí | | Recurso específico al que se aplica el permiso (route, vehicle, driver, dispatch) |
| action | character varying(50) | Sí | | Acción sobre el recurso (view, create, update, delete, approve) |

**Clave primaria:** permission_id
**Claves foraneas:** Ninguna
**Indices y restricciones:** 
- chk_permission_module: Verifica que el módulo esté en la lista permitida
- permission_code_key: Único para el código del permiso
- permission_pkey: Clave primaria
- idx_permission_code: Índice en el código del permiso
- idx_permission_module: Índice en el módulo y estado del permiso
**Triggers:** 
- trg_permissions_change: Notifica cambios en el estado del permiso
**Particionado:** Ninguno
**Observaciones:** Ninguna
