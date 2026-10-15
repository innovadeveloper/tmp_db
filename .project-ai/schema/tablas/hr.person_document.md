## hr.person_document
**Tipo:** tabla
**Proposito:** Almacena información sobre los documentos personales de los individuos, incluyendo su tipo, número, entidad emisora, fecha de emisión, fecha de vencimiento, archivo asociado, estado, verificación y notas.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| person_document_id | bigint | No | Sí | Identificador único del documento personal. |
| person_id | integer | No | Sí | Identificador del individuo al que pertenece el documento. |
| document_type_id | integer | No | Sí | Identificador del tipo de documento. |
| document_number | character varying(100) | Sí | Sí | Número del documento. |
| issuing_entity | character varying(255) | Sí | Sí | Entidad que emitió el documento. |
| issue_date | date | Sí | Sí | Fecha de emisión del documento. |
| expiry_date | date | Sí | Sí | Fecha de vencimiento del documento. |
| file_id | bigint | Sí | Sí | Identificador del archivo asociado al documento. |
| status | character varying(20) | No | 'VALID' | Estado del documento (VALID, EXPIRED, PENDING, REJECTED). |
| verified_by | bigint | Sí | Sí | Identificador del usuario que verificó el documento. |
| verified_at | timestamp with time zone | Sí | Sí | Fecha y hora en que se verificó el documento. |
| notes | text | Sí | Sí | Notas adicionales sobre el documento. |
| created_at | timestamp with time zone | No | now() | Fecha y hora de creación del registro. |
| updated_at | timestamp with time zone | No | now() | Fecha y hora de la última actualización del registro. |

**Clave primaria:** person_document_id
**Claves foraneas:** 
- person_id -> hr.person.person_id
- document_type_id -> shared.document_type.document_type_id
- file_id -> shared.file_storage.file_id
- verified_by -> identity."user".user_id
**Indices y restricciones:** 
- person_document_pkey: Clave primaria en person_document_id
- uq_person_document_type: Único por person_id y document_type_id
- idx_person_doc_expiry: Índice en expiry_date y status para documentos válidos
- idx_person_doc_person: Índice en person_id y status
- idx_person_doc_type: Índice en document_type_id
- chk_person_doc_status: Restricción CHECK para el estado del documento
**Triggers:** Por confirmar
**Particionado:** Por confirmar
**Observaciones:** No hay problemas evidentes de diseño.
