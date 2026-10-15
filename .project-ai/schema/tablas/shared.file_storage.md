## shared.file_storage
**Tipo:** tabla
**Proposito:** Almacena metadatos y ubicación de archivos adjuntos como documentos, fotos y evidencias.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| file_id | bigint | No | nextval('shared.file_storage_file_id_seq'::regclass) | Identificador único del archivo |
| original_filename | character varying(255) | No | | Nombre original del archivo subido |
| stored_filename | character varying(255) | No | | Nombre UUID en el almacenamiento |
| file_path | character varying(500) | No | | Ruta del archivo en el almacenamiento |
| file_size_bytes | bigint | No | | Tamaño del archivo en bytes |
| mime_type | character varying(100) | Sí | | Tipo MIME del archivo |
| storage_type | character varying(20) | No | 'LOCAL' | Tipo de almacenamiento: LOCAL, S3, AZURE, GCS |
| uploaded_by | bigint | Sí | | ID del usuario que subió el archivo |
| uploaded_at | timestamp with time zone | No | now() | Fecha y hora de subida del archivo |
| is_public | boolean | No | false | Indica si el archivo es público |
| created_at | timestamp with time zone | No | now() | Fecha y hora de creación del archivo |

**Clave primaria:** file_id

**Claves foraneas:** uploaded_by -> identity."user"(user_id)

**Indices y restricciones:** 
- chk_file_size_positive: Verifica que el tamaño del archivo sea positivo
- chk_file_storage_type: Verifica que el tipo de almacenamiento sea uno de los permitidos (LOCAL, S3, AZURE, GCS)
- idx_file_storage_mime: Índice B-tree en mime_type
- idx_file_storage_original_trgm: Índice GIN en original_filename para búsqueda por trigramas
- idx_file_storage_public: Índice B-tree en is_public y uploaded_at para búsqueda de archivos públicos recientes
- idx_file_storage_type: Índice B-tree en storage_type
- idx_file_storage_uploaded_at: Índice B-tree en uploaded_at para búsqueda de archivos recientes
- idx_file_storage_uploaded_by: Índice B-tree en uploaded_by para búsqueda de archivos subidos por un usuario específico

**Triggers:** No se especifican en el SQL proporcionado

**Particionado:** No se especifica en el SQL proporcionado

**Observaciones:** 
- La columna `mime_type` es opcional y puede ser nula.
- La columna `uploaded_by` es opcional y puede ser nula, lo que permite almacenar archivos sin asociarlos a un usuario específico.
- La columna `is_public` se utiliza para marcar archivos como públicos, lo que puede ser útil para recursos como logos y archivos de contenido general.
