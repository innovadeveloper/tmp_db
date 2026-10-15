## identity.user_session
**Tipo:** tabla
**Proposito:** Almacena información sobre las sesiones activas de los usuarios, incluyendo detalles como el token de sesión, la dirección IP, el agente del usuario, fechas de inicio y expiración, y el estado de actividad.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| session_id | bigint | No | nextval('identity.user_session_session_id_seq'::regclass) | Identificador único de la sesión. |
| user_id | bigint | No | Ninguna | Identificador del usuario asociado con la sesión. |
| token | character varying(500) | No | Ninguna | Token de sesión, almacenado hasheado en producción. |
| ip_address | inet | Sí | Ninguna | Dirección IP desde la que se inició la sesión. |
| user_agent | text | Sí | Ninguna | Información sobre el agente del usuario que inició la sesión. |
| started_at | timestamp with time zone | Sí | now() | Fecha y hora en que la sesión comenzó. |
| last_activity_at | timestamp with time zone | Sí | now() | Fecha y hora de la última actividad en la sesión. |
| expires_at | timestamp with time zone | No | Ninguna | Fecha y hora en que la sesión expirará. |
| is_active | boolean | Sí | true | Indica si la sesión está activa. |
| created_at | timestamp with time zone | Sí | now() | Fecha y hora en que se creó la sesión. |

**Clave primaria:** session_id
**Claves foraneas:** user_id -> identity."user".user_id
**Indices y restricciones:** 
- chk_session_dates: Verifica que la fecha de expiración sea posterior a la fecha de inicio.
- user_session_token_key: Único para el token de sesión.
- idx_session_active_recent: Índice para buscar sesiones activas recientes de un usuario.
- idx_session_expires: Índice para buscar sesiones por fecha de expiración.
- idx_session_ip: Índice para buscar sesiones por dirección IP.
- idx_session_token: Índice para buscar sesiones por token.
- idx_session_user_active: Índice para buscar sesiones activas de un usuario.

**Triggers:** Ninguno

**Particionado:** Ninguno

**Observaciones:** Ninguna
