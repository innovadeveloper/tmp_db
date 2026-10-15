## fleet.vehicle_document
**Tipo:** tabla
**Proposito:** Almacena información sobre los documentos asociados a los vehículos, incluyendo su tipo, número, entidad emisora, fechas de emisión y vencimiento, estado, verificación y notas.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| vehicle_document_id | bigint | No | nextval('fleet.vehicle_document_vehicle_document_id_seq'::regclass) | Identificador único del documento del vehículo |
| vehicle_id | integer | No | Por confirmar | Identificador del vehículo al que pertenece el documento |
| document_type_id | integer | No | Por confirmar | Identificador del tipo de documento |
| document_number | character varying(100) | Sí | Por confirmar | Número del documento |
| issuing_entity | character varying(255) | Sí | Por confirmar | Entidad emisora del documento |
| issue_date | date | Sí | Por confirmar | Fecha de emisión del documento |
| expiry_date | date | Sí | Por confirmar | Fecha de vencimiento del documento |
| file_id | bigint | Sí | Por confirmar | Identificador del archivo asociado al documento |
| status | character varying(20) | No | 'VALID'::character varying | Estado del documento (VALID, EXPIRED, PENDING, REJECTED) |
| verified_by | bigint | Sí | Por confirmar | Identificador del usuario que verificó el documento |
| verified_at | timestamp with time zone | Sí | now() | Fecha y hora en que se verificó el documento |
| notes | text | Sí | Por confirmar | Notas adicionales sobre el documento |
| created_at | timestamp with time zone | No | now() | Fecha y hora de creación del registro |
| updated_at | timestamp with time zone | No | now() | Fecha y hora de la última actualización del registro |

**Clave primaria:** vehicle_document_id
**Claves foraneas:** 
- vehicle_id -> fleet.vehicle(vehicle_id)
- document_type_id -> shared.document_type(document_type_id)
- file_id -> shared.file_storage(file_id)
- verified_by -> identity."user"(user_id)
**Indices y restricciones:** 
- chk_vehicle_doc_dates: Verifica que la fecha de vencimiento sea posterior a la fecha de emisión
- chk_vehicle_doc_status: Verifica que el estado del documento sea uno de los permitidos (VALID, EXPIRED, PENDING, REJECTED)
- uq_vehicle_document_type: Evita duplicados de documentos del mismo tipo para el mismo vehículo
- idx_vehicle_doc_critical_expired: Índice para documentos expirados críticos
- idx_vehicle_doc_expiry: Índice para documentos válidos por fecha de vencimiento
- idx_vehicle_doc_type: Índice para documentos por tipo y estado
- idx_vehicle_doc_vehicle: Índice para documentos por vehículo y estado
- idx_vehicle_doc_verified: Índice para documentos por fecha de verificación descendente
**Triggers:** No se especifican en el SQL proporcionado
**Particionado:** No se especifica en el SQL proporcionado
**Observaciones:** No se identifican problemas de diseño evidentes
