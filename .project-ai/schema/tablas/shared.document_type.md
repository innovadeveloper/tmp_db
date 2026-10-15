## shared.document_type
**Tipo:** tabla  
**Proposito:** Almacena información sobre los tipos de documentos, incluyendo su código, nombre, descripción, requisitos específicos y estado de activación.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| document_type_id | integer | No | nextval('shared.document_type_document_type_id_seq'::regclass) | Identificador único del tipo de documento |
| code | character varying(50) | No | Por confirmar | Código único del tipo de documento |
| name | character varying(100) | No | Por confirmar | Nombre descriptivo del tipo de documento |
| description | text | Sí | Por confirmar | Descripción detallada del tipo de documento |
| is_mandatory | boolean | Sí | true | Indica si el tipo de documento es obligatorio |
| requires_expiry | boolean | Sí | false | Indica si el tipo de documento requiere una fecha de vencimiento |
| alert_days_before | integer | Sí | Por confirmar | Días antes de la fecha de vencimiento para generar una alerta |
| restriction_type | character varying(20) | Sí | Por confirmar | Tipo de restricción aplicable al tipo de documento |
| is_active | boolean | Sí | true | Indica si el tipo de documento está activo |
| created_at | timestamp with time zone | Sí | now() | Fecha y hora de creación del tipo de documento |
| entity_type | character varying(20) | Sí | 'GENERAL' | Tipo de entidad a la que se aplica el tipo de documento |

**Clave primaria:** document_type_id

**Claves foraneas:** Ninguna

**Indices y restricciones:**  
- chk_document_alert_days: Asegura que si se especifican días de alerta, deben ser mayores que 0.
- chk_document_expiry_alert: Asegura que si se requiere vencimiento, también se especifican días de alerta.
- chk_document_restriction_type: Asegura que el tipo de restricción sea uno de los permitidos (CRITICAL, WARNING, NONE).
- document_type_code_key: Índice único en el código del tipo de documento.
- document_type_pkey: Clave primaria en el identificador del tipo de documento.
- idx_document_type_code: Índice en el código del tipo de documento.
- idx_document_type_critical: Índice en el tipo de restricción y estado activo para tipos críticos.
- idx_document_type_expiry: Índice en la requiere vencimiento y estado activo para tipos que requieren vencimiento.
- idx_document_type_mandatory: Índice en el tipo de documento y estado activo para tipos obligatorios.

**Triggers:** Ninguno

**Particionado:** Ninguno

**Observaciones:**  
- La columna `code` debería tener un valor por defecto para evitar valores nulos.
- La columna `alert_days_before` debería tener un valor por defecto para evitar valores nulos.
- La columna `restriction_type` debería tener un valor por defecto para evitar valores nulos.
