## identity.permission_template
**Tipo:** tabla
**Proposito:** Almacena plantillas de permisos para diferentes tipos de roles en el sistema.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| template_id | integer | No | nextval('identity.permission_template_template_id_seq'::regclass) | Identificador único de la plantilla de permiso. |
| name | character varying(100) | No | | Nombre de la plantilla de permiso. |
| description | text | Sí | | Descripción detallada de la plantilla de permiso. |
| role_type | character varying(50) | Sí | | Tipo de rol al que se asigna la plantilla de permiso (ADMIN, SUPERVISOR, DISPATCHER, CASHIER, FLEET_MANAGER, HR_MANAGER, OPERATOR, AUDITOR). |
| is_active | boolean | Sí | true | Indica si la plantilla de permiso está activa. |
| created_at | timestamp with time zone | Sí | now() | Fecha y hora en que se creó la plantilla de permiso. |

**Clave primaria:** template_id

**Claves foraneas:** Ninguna

**Indices y restricciones:** 
- chk_template_role_type: Verifica que el valor de role_type sea uno de los permitidos.
- idx_template_role_type: Índice B-tree en role_type y is_active para mejorar la eficiencia de las consultas que filtren por estos campos.

**Triggers:** Ninguno

**Particionado:** Ninguno

**Observaciones:** La columna role_type tiene un tipo de dato VARCHAR(50) pero solo acepta valores específicos definidos en la restricción chk_template_role_type.
