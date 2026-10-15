## identity.activity_log_2026_08
**Tipo:** tabla
**Proposito:** Almacena registros de actividades realizadas por usuarios, incluyendo detalles sobre la acción, recurso afectado, dirección IP, agente del usuario, cambios realizados, estado de la acción y mensajes de error.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| log_id | bigint | No | nextval('identity.activity_log_log_id_seq'::regclass) | Identificador único de cada registro de actividad. |
| user_id | bigint | Sí | Ninguna | Identificador del usuario que realizó la acción. |
| action | character varying(100) | No | Ninguna | Descripción de la acción realizada. |
| resource_type | character varying(100) | Sí | Ninguna | Tipo de recurso afectado por la acción. |
| resource_id | bigint | Sí | Ninguna | Identificador del recurso afectado por la acción. |
| ip_address | inet | Sí | Ninguna | Dirección IP desde la que se realizó la acción. |
| user_agent | text | Sí | Ninguna | Información sobre el agente del usuario que realizó la acción. |
| changes | jsonb | Sí | Ninguna | Cambios realizados durante la acción, en formato JSONB. |
| status | character varying(20) | Sí | Ninguna | Estado de la acción (SUCCESS, FAILED, PARTIAL, PENDING). |
| error_message | text | Sí | Ninguna | Mensaje de error asociado a la acción, si es que ocurrió un error. |
| created_at | timestamp with time zone | No | now() | Fecha y hora en que se creó el registro de actividad. |

**Clave primaria:** log_id, created_at
**Claves foraneas:** Ninguna
**Indices y restricciones:** 
- chk_activity_status: Verifica que el estado de la acción sea uno de los permitidos (SUCCESS, FAILED, PARTIAL, PENDING).
- activity_log_2026_08_action_created_at_idx: Índice B-tree en action y created_at para mejorar la búsqueda de acciones por tipo y fecha.
- activity_log_2026_08_changes_idx: Índice GIN en changes para búsqueda de cambios específicos.
- activity_log_2026_08_resource_type_resource_id_idx: Índice B-tree en resource_type y resource_id para mejorar la búsqueda de acciones por recurso.
- activity_log_2026_08_status_created_at_idx: Índice B-tree en status y created_at para mejorar la búsqueda de acciones fallidas por fecha.
- activity_log_2026_08_user_id_created_at_idx: Índice B-tree en user_id y created_at para mejorar la búsqueda de acciones por usuario y fecha.

**Triggers:** No se especifican en el SQL proporcionado.
**Particionado:** No se especifica en el SQL proporcionado.
**Observaciones:** No se identificaron problemas de diseño evidentes.
