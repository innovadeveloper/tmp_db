## identity.login_attempt_2026_02
**Tipo:** tabla
**Proposito:** Almacena los intentos de inicio de sesión del sistema, incluyendo detalles sobre el usuario, la dirección IP, el agente del usuario, el resultado del intento y la razón de la falla si es aplicable.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| attempt_id | bigint | No | nextval('identity.login_attempt_attempt_id_seq'::regclass) | Identificador único del intento de inicio de sesión. |
| username | character varying(100) | No | Por confirmar | Nombre de usuario que intentó iniciar sesión. |
| ip_address | inet | No | Por confirmar | Dirección IP desde la que se intentó iniciar sesión. |
| user_agent | text | Sí | Por confirmar | Información sobre el agente del usuario que realizó el intento. |
| success | boolean | No | Por confirmar | Indica si el intento de inicio de sesión fue exitoso. |
| failure_reason | character varying(100) | Sí | Por confirmar | Razón de la falla del intento de inicio de sesión, si no fue exitoso. |
| attempted_at | timestamp with time zone | No | now() | Fecha y hora en que se realizó el intento de inicio de sesión. |

**Clave primaria:** attempt_id, attempted_at
**Claves foraneas:** Ninguna
**Indices y restricciones:** 
- chk_login_failure_reason: Verifica que si el inicio de sesión fue exitoso, la razón de la falla no debe estar definida.
- chk_login_failure_values: Verifica que la razón de la falla, si está definida, debe ser uno de los valores permitidos.
- login_attempt_2026_02_ip_address_attempted_at_idx: Índice en ip_address y attempted_at para mejorar la eficiencia de las consultas filtradas por dirección IP y fecha.
- login_attempt_2026_02_ip_address_attempted_at_idx1: Índice alternativo en ip_address y attempted_at para mejorar la eficiencia de las consultas filtradas por dirección IP, fecha y resultado exitoso.
- login_attempt_2026_02_success_attempted_at_idx: Índice en success y attempted_at para mejorar la eficiencia de las consultas filtradas por resultado exitoso y fecha.
- login_attempt_2026_02_username_attempted_at_idx: Índice en username y attempted_at para mejorar la eficiencia de las consultas filtradas por nombre de usuario y fecha.
- login_attempt_2026_02_username_attempted_at_idx1: Índice alternativo en username y attempted_at para mejorar la eficiencia de las consultas filtradas por nombre de usuario, fecha y resultado exitoso.

**Triggers:** Por confirmar
**Particionado:** Por confirmar
**Observaciones:** Las restricciones y índices están diseñados para optimizar las consultas frecuentes que se realizarán sobre los intentos de inicio de sesión, especialmente filtradas por dirección IP, nombre de usuario y resultado exitoso.
