## identity.login_attempt_2026_09
**Tipo:** tabla
**Proposito:** Almacena los intentos de inicio de sesión de los usuarios.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| attempt_id | bigint | No | nextval('identity.login_attempt_attempt_id_seq'::regclass) | Identificador único del intento de inicio de sesión. |
| username | character varying(100) | No | | Nombre de usuario intentando iniciar sesión. |
| ip_address | inet | No | | Dirección IP desde la que se intenta iniciar sesión. |
| user_agent | text | Sí | | Información sobre el navegador o cliente que intenta iniciar sesión. |
| success | boolean | No | | Indica si el intento de inicio de sesión fue exitoso. |
| failure_reason | character varying(100) | Sí | | Razón del fallo en el intento de inicio de sesión. |
| attempted_at | timestamp with time zone | No | now() | Fecha y hora en que se intentó iniciar sesión. |

**Clave primaria:** attempt_id, attempted_at

**Claves foraneas:** Ninguna

**Indices y restricciones:**
- chk_login_failure_reason: Asegura que si el inicio de sesión fue exitoso, no haya razón de fallo.
- chk_login_failure_values: Valida que la razón de fallo esté en la lista permitida.
- login_attempt_2026_09_ip_address_attempted_at_idx: Índice para búsqueda por dirección IP y fecha/hora.
- login_attempt_2026_09_ip_address_attempted_at_idx1: Índice para búsqueda por dirección IP y fecha/hora, filtrando solo los intentos fallidos.
- login_attempt_2026_09_success_attempted_at_idx: Índice para búsqueda por éxito y fecha/hora, filtrando solo los intentos fallidos.
- login_attempt_2026_09_username_attempted_at_idx: Índice para búsqueda por nombre de usuario y fecha/hora.
- login_attempt_2026_09_username_attempted_at_idx1: Índice para búsqueda por nombre de usuario y fecha/hora, filtrando solo los intentos fallidos.

**Triggers:** Ninguno

**Particionado:** Ninguno

**Observaciones:** El diseño es adecuado para almacenar y buscar intentos de inicio de sesión de manera eficiente. Las restricciones aseguran la integridad de los datos.
