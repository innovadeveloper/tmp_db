## identity.activity_log_2026_02
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
| changes | jsonb | Sí | Ninguna | Cambios realizados en el recurso, en formato JSON. |
| status | character varying(20) | Sí | Ninguna | Estado del registro de actividad (SUCCESS, FAILED, PARTIAL, PENDING). |
| error_message | text | Sí | Ninguna | Mensaje de error asociado al registro, si es necesario. |
| created_at | timestamp with time zone | No | now() | Fecha y hora en que se creó el registro de actividad. |

**Clave primaria:** log_id, created_at
**Claves foraneas:** Ninguna
**Indices y restricciones:** 
- chk_activity_status: Verifica que el estado de la actividad sea uno de los permitidos (SUCCESS, FAILED, PARTIAL, PENDING).
- activity_log_2026_02_action_created_at_idx: Índice por acción y fecha de creación.
- activity_log_2026_02_changes_idx: Índice GIN para búsqueda de cambios.
- activity_log_2026_02_resource_type_resource_id_idx: Índice por tipo de recurso y identificador de recurso.
- activity_log_2026_02_status_created_at_idx: Índice por estado y fecha de creación, filtrado para solo registros con estado FAILED.
- activity_log_2026_02_user_id_created_at_idx: Índice por usuario y fecha de creación.

**Triggers:** Ninguna
**Particionado:** Ninguna
**Observaciones:** Ninguna
