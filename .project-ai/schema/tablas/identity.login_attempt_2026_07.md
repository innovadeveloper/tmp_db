## identity.login_attempt_2026_07
**Tipo:** tabla
**Proposito:** Almacena los intentos de inicio de sesión del sistema.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| attempt_id | bigint | No | nextval('identity.login_attempt_attempt_id_seq'::regclass) | Identificador único del intento de inicio de sesión. |
| username | character varying(100) | No | | Nombre de usuario intentando iniciar sesión. |
| ip_address | inet | No | | Dirección IP desde la que se intenta iniciar sesión. |
| user_agent | text | Sí | | Información sobre el navegador o cliente utilizado. |
| success | boolean | No | | Indica si el intento de inicio de sesión fue exitoso. |
| failure_reason | character varying(100) | Sí | | Razón del fallo del intento de inicio de sesión. |
| attempted_at | timestamp with time zone | No | now() | Fecha y hora en que se intentó iniciar sesión. |

**Clave primaria:** attempt_id, attempted_at

**Claves foraneas:** Ninguna

**Indices y restricciones:** 
- chk_login_failure_reason: Verifica que si el inicio de sesión fue exitoso, no haya razón de fallo. Si el inicio de sesión falló, la razón de fallo debe estar en la lista permitida.
- chk_login_failure_values: Valida que la razón de fallo esté en la lista permitida.

**Triggers:** Ninguno

**Particionado:** Ninguno

**Observaciones:** 
- La tabla está diseñada para almacenar intentos de inicio de sesión de un año específico (2026).
- Los índices están optimizados para búsquedas por dirección IP, nombre de usuario y estado de éxito, lo que facilita la realización de consultas frecuentes sobre estos campos.
