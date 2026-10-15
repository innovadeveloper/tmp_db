## identity.activity_log_2026_09
**Tipo:** tabla
**Proposito:** Almacena registros de actividades realizadas por usuarios, incluyendo detalles sobre la acción, recurso afectado, dirección IP, agente de usuario, cambios realizados, estado y mensajes de error.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| log_id | bigint | No | nextval('identity.activity_log_log_id_seq'::regclass) | Identificador único de cada registro de actividad. |
| user_id | bigint | Sí | Ninguna | Identificador del usuario que realizó la acción. |
| action | character varying(100) | No | Ninguna | Descripción de la acción realizada. |
| resource_type | character varying(100) | Sí | Ninguna | Tipo de recurso afectado por la acción. |
| resource_id | bigint | Sí | Ninguna | Identificador del recurso afectado por la acción. |
| ip_address | inet | Sí | Ninguna | Dirección IP desde la que se realizó la acción. |
| user_agent | text | Sí | Ninguna | Información sobre el agente de usuario que realizó la acción. |
| changes | jsonb | Sí | Ninguna | Cambios realizados durante la acción, en formato JSONB. |
| status | character varying(20) | Sí | Ninguna | Estado de la acción (SUCCESS, FAILED, PARTIAL, PENDING). |
| error_message | text | Sí | Ninguna | Mensaje de error asociado a la acción, si es necesario. |
| created_at | timestamp with time zone | No | now() | Fecha y hora en que se creó el registro de actividad. |

**Clave primaria:** log_id, created_at
**Claves foraneas:** Ninguna
**Indices y restricciones:** 
- chk_activity_status: Verifica que el estado de la acción sea uno de los permitidos (SUCCESS, FAILED, PARTIAL, PENDING).
- activity_log_2026_09_action_created_at_idx: Índice en action y created_at para mejorar la búsqueda de registros por acción y fecha.
- activity_log_2026_09_changes_idx: Índice GIN en changes para búsqueda de cambios específicos.
- activity_log_2026_09_resource_type_resource_id_idx: Índice en resource_type y resource_id para mejorar la búsqueda de registros por recurso.
- activity_log_2026_09_status_created_at_idx: Índice en status y created_at para mejorar la búsqueda de registros por estado y fecha, pero solo para registros con estado FAILED.
- activity_log_2026_09_user_id_created_at_idx: Índice en user_id y created_at para mejorar la búsqueda de registros por usuario y fecha.

**Triggers:** Por confirmar
**Particionado:** Por confirmar
**Observaciones:** La tabla incluye un índice GIN en la columna changes, lo que puede ser útil para consultas complejas sobre los cambios realizados, pero también puede aumentar el tiempo de inserción y mantenimiento de índices.
