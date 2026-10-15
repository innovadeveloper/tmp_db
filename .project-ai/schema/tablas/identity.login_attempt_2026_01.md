## identity.login_attempt_2026_01
**Tipo:** tabla
**Proposito:** Almacena los intentos de inicio de sesión del sistema para el año 2026.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| attempt_id | bigint | No | nextval('identity.login_attempt_attempt_id_seq'::regclass) | Identificador único del intento de inicio de sesión. |
| username | character varying(100) | No | | Nombre de usuario intentando iniciar sesión. |
| ip_address | inet | No | | Dirección IP desde la que se intenta iniciar sesión. |
| user_agent | text | Sí | | Información sobre el navegador o cliente que intenta iniciar sesión. |
| success | boolean | No | | Indica si el intento de inicio de sesión fue exitoso. |
| failure_reason | character varying(100) | Sí | | Razón del fallo del intento de inicio de sesión, si no fue exitoso. |
| attempted_at | timestamp with time zone | No | now() | Fecha y hora en que se intentó iniciar sesión. |

**Clave primaria:** attempt_id, attempted_at
**Claves foraneas:** Ninguna
**Indices y restricciones:** 
- chk_login_failure_reason: Verifica que si el inicio de sesión fue exitoso, la razón del fallo no debe estar definida.
- chk_login_failure_values: Verifica que la razón del fallo esté en la lista permitida si el inicio de sesión no fue exitoso.
- login_attempt_2026_01_ip_address_attempted_at_idx: Índice en ip_address y attempted_at para mejorar la eficiencia de las consultas filtradas por dirección IP y fecha.
- login_attempt_2026_01_ip_address_attempted_at_idx1: Índice adicional para mejorar la eficiencia de las consultas filtradas por dirección IP, fecha y resultado del intento.
- login_attempt_2026_01_success_attempted_at_idx: Índice en success y attempted_at para mejorar la eficiencia de las consultas filtradas por resultado del intento y fecha.
- login_attempt_2026_01_username_attempted_at_idx: Índice en username y attempted_at para mejorar la eficiencia de las consultas filtradas por nombre de usuario y fecha.
- login_attempt_2026_01_username_attempted_at_idx1: Índice adicional para mejorar la eficiencia de las consultas filtradas por nombre de usuario, fecha y resultado del intento.

**Triggers:** Ninguno
**Particionado:** Ninguno
**Observaciones:** La tabla incluye índices para mejorar la eficiencia de las consultas comunes, como filtrar por dirección IP, nombre de usuario y resultado del intento. Las restricciones garantizan la integridad de los datos, asegurando que las razones de fallo sean válidas y que solo los intentos fallidos tengan una razón de fallo definida.
