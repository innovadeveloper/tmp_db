## identity.login_attempt
**Tipo:** tabla
**Proposito:** Almacena los intentos de inicio de sesión de los usuarios, incluyendo su éxito o fracaso, la razón del fracaso, la dirección IP y el agente del usuario.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| attempt_id | bigint | No | nextval('identity.login_attempt_attempt_id_seq'::regclass) | Identificador único del intento de inicio de sesión. |
| username | character varying(100) | No | Por confirmar | Nombre de usuario que intentó iniciar sesión. |
| ip_address | inet | No | Por confirmar | Dirección IP desde la que se intentó iniciar sesión. |
| user_agent | text | Sí | Por confirmar | Información sobre el agente del usuario que intentó iniciar sesión. |
| success | boolean | No | Por confirmar | Indica si el intento de inicio de sesión fue exitoso o no. |
| failure_reason | character varying(100) | Sí | Por confirmar | Razón del fracaso del intento de inicio de sesión. Valores permitidos: 'INVALID_CREDENTIALS', 'ACCOUNT_LOCKED', 'ACCOUNT_DISABLED', 'IP_BLOCKED', 'MFA_REQUIRED', 'MFA_FAILED', 'SESSION_EXPIRED', 'UNAUTHORIZED'. |
| attempted_at | timestamp with time zone | No | now() | Fecha y hora en que se intentó iniciar sesión. |

**Clave primaria:** attempt_id, attempted_at
**Claves foraneas:** Ninguna
**Indices y restricciones:** 
- chk_login_failure_reason: Verifica que si el inicio de sesión fue exitoso, la razón del fracaso debe ser nula.
- chk_login_failure_values: Verifica que la razón del fracaso, si existe, sea uno de los valores permitidos.
- idx_login_failed: Índice para búsquedas de intentos de inicio de sesión fallidos, ordenados por fecha y hora descendente.
- idx_login_failed_ip: Índice para búsquedas de intentos de inicio de sesión fallidos por dirección IP, ordenados por fecha y hora descendente.
- idx_login_failed_user: Índice para búsquedas de intentos de inicio de sesión fallidos por nombre de usuario, ordenados por fecha y hora descendente.
- idx_login_ip_date: Índice para búsquedas de intentos de inicio de sesión por dirección IP y fecha y hora.
- idx_login_username_date: Índice para búsquedas de intentos de inicio de sesión por nombre de usuario y fecha y hora.
**Triggers:** Por confirmar
**Particionado:** identity.login_attempt_2026_01, identity.login_attempt_2026_02, identity.login_attempt_2026_06, identity.login_attempt_2026_07, identity.login_attempt_2026_08, identity.login_attempt_2026_09
**Observaciones:** La tabla está particionada por rango de fecha y hora, lo que facilita la gestión y consulta de datos históricos.
