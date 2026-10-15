## identity.permission_template_detail
**Tipo:** tabla
**Proposito:** Almacena los detalles de las plantillas de permisos, relacionando plantillas y permisos específicos.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| template_detail_id | bigint | No | nextval('identity.permission_template_detail_template_detail_id_seq'::regclass) | Identificador único de la detalle de la plantilla de permiso. |
| template_id | integer | No | Por confirmar | Identificador de la plantilla de permiso. |
| permission_id | integer | No | Por confirmar | Identificador del permiso. |
| created_at | timestamp with time zone | Sí | now() | Fecha y hora de creación del detalle de la plantilla de permiso. |

**Clave primaria:** template_detail_id

**Claves foraneas:** 
- permission_id -> identity.permission.permission_id
- template_id -> identity.permission_template.template_id

**Indices y restricciones:** 
- uq_template_permission: Único para asegurar que no haya duplicados de plantilla y permiso.
- idx_template_detail_permission: Índice en permission_id para mejorar la eficiencia de las consultas.
- idx_template_detail_template: Índice en template_id para mejorar la eficiencia de las consultas.

**Triggers:** 
- Por confirmar: No se especifican triggers en el SQL proporcionado.

**Particionado:** 
- Por confirmar: No se especifica particionado en el SQL proporcionado.

**Observaciones:** 
- La tabla no tiene restricciones adicionales ni triggers específicos.
