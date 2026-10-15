## identity.activity_log_2026_01
**Tipo:** tabla
**Proposito:** Almacena registros de actividades realizadas por usuarios en el sistema.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| log_id | bigint | No | nextval('identity.activity_log_log_id_seq'::regclass) | Identificador único de cada registro de actividad. |
| user_id | bigint | Sí | Ninguna | Identificador del usuario que realizó la acción. |
| action | character varying(100) | No | Ninguna | Descripción de la acción realizada. |
| resource_type | character varying(100) | Sí | Ninguna | Tipo de recurso afectado por la acción. |
| resource_id | bigint | Sí | Ninguna | Identificador del recurso afectado por la acción. |
| ip_address | inet | Sí | Ninguna | Dirección IP desde la que se realizó la acción. |
| user_agent | text | Sí | Ninguna | Información sobre el navegador o cliente que realizó la acción. |
| changes | jsonb | Sí | Ninguna | Cambios realizados en el recurso, en formato JSONB. |
| status | character varying(20) | Sí | Ninguna | Estado del registro de actividad (SUCCESS, FAILED, PARTIAL, PENDING). |
| error_message | text | Sí | Ninguna | Mensaje de error asociado al registro de actividad. |
| created_at | timestamp with time zone | No | now() | Fecha y hora en que se creó el registro de actividad. |

**Clave primaria:** log_id, created_at
**Claves foraneas:** Ninguna
**Indices y restricciones:** 
- chk_activity_status: Verifica que el estado del registro de actividad sea uno de los permitidos (SUCCESS, FAILED, PARTIAL, PENDING).
- activity_log_2026_01_action_created_at_idx: Índice en action y created_at para mejorar la búsqueda de actividades por acción y fecha.
- activity_log_2026_01_changes_idx: Índice GIN en changes para mejorar la búsqueda de cambios en el recurso.
- activity_log_2026_01_resource_type_resource_id_idx: Índice en resource_type y resource_id para mejorar la búsqueda de actividades por tipo de recurso y identificador.
- activity_log_2026_01_status_created_at_idx: Índice en status y created_at para mejorar la búsqueda de actividades fallidas por fecha.
- activity_log_2026_01_user_id_created_at_idx: Índice en user_id y created_at para mejorar la búsqueda de actividades por usuario y fecha.

**Triggers:** Ninguno
**Particionado:** Ninguno
**Observaciones:** Ninguna
