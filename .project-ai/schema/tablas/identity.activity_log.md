## identity.activity_log
**Tipo:** tabla
**Proposito:** Almacena un registro de todas las acciones críticas realizadas por los usuarios, incluyendo detalles sobre la acción, el recurso afectado, la dirección IP y el agente del usuario.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| log_id | bigint | No | nextval('identity.activity_log_log_id_seq'::regclass) | Identificador único de cada registro de actividad. |
| user_id | bigint | Sí | Ninguna | Identificador del usuario que realizó la acción. |
| action | character varying(100) | No | Ninguna | Descripción de la acción realizada. |
| resource_type | character varying(100) | Sí | Ninguna | Tipo de recurso afectado por la acción. |
| resource_id | bigint | Sí | Ninguna | Identificador del recurso afectado. |
| ip_address | inet | Sí | Ninguna | Dirección IP desde la que se realizó la acción. |
| user_agent | text | Sí | Ninguna | Información sobre el agente del usuario que realizó la acción. |
| changes | jsonb | Sí | Ninguna | Cambios realizados en el recurso, en formato JSON. |
| status | character varying(20) | Sí | Ninguna | Estado de la acción (SUCCESS, FAILED, PARTIAL, PENDING). |
| error_message | text | Sí | Ninguna | Mensaje de error asociado a la acción, si es necesario. |
| created_at | timestamp with time zone | No | now() | Fecha y hora en que se creó el registro de actividad. |

**Clave primaria:** log_id, created_at

**Claves foraneas:** user_id -> identity."user".user_id

**Indices y restricciones:** 
- idx_activity_action: Índice B-tree en action y created_at para mejorar la búsqueda de acciones recientes.
- idx_activity_changes: Índice GIN en changes para facilitar búsquedas complejas en los cambios.
- idx_activity_resource: Índice B-tree en resource_type y resource_id para mejorar la búsqueda de acciones por recurso.
- idx_activity_failed: Índice B-tree en status y created_at para mejorar la búsqueda de acciones fallidas recientes.
- idx_activity_user_date: Índice B-tree en user_id y created_at para mejorar la búsqueda de acciones por usuario recientes.
- chk_activity_status: Restricción CHECK para asegurar que el estado de la acción sea uno de los permitidos (SUCCESS, FAILED, PARTIAL, PENDING).

**Triggers:** Por confirmar

**Particionado:** identity.activity_log_2026_01, identity.activity_log_2026_02, identity.activity_log_2026_06, identity.activity_log_2026_07, identity.activity_log_2026_08, identity.activity_log_2026_09

**Observaciones:** La tabla está particionada por rango de fecha, lo que facilita la gestión y el análisis de datos históricos.
