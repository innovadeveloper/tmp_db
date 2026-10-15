## identity.login_attempt_2026_08
**Tipo:** tabla
**Proposito:** Almacena los intentos de inicio de sesión del sistema.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| attempt_id | bigint | No | nextval('identity.login_attempt_attempt_id_seq'::regclass) | Identificador único del intento de inicio de sesión. |
| username | character varying(100) | No | Por confirmar | Nombre de usuario que intentó iniciar sesión. |
| ip_address | inet | No | Por confirmar | Dirección IP desde la que se intentó iniciar sesión. |
| user_agent | text | Sí | Por confirmar | Información sobre el navegador o cliente que intentó iniciar sesión. |
| success | boolean | No | Por confirmar | Indica si el intento de inicio de sesión fue exitoso. |
| failure_reason | character varying(100) | Sí | Por confirmar | Razón del fallo en el intento de inicio de sesión, si no fue exitoso. |
| attempted_at | timestamp with time zone | No | now() | Fecha y hora en que se intentó iniciar sesión. |

**Clave primaria:** attempt_id, attempted_at

**Claves foraneas:** Ninguna

**Indices y restricciones:** 
- chk_login_failure_reason: Verifica que si el inicio de sesión fue exitoso, no haya razón de fallo. Si el inicio de sesión no fue exitoso, debe haber una razón de fallo.
- chk_login_failure_values: Verifica que la razón de fallo esté en la lista permitida.

**Triggers:** Por confirmar

**Particionado:** Por confirmar

**Observaciones:** La tabla incluye índices para mejorar el rendimiento de consultas frecuentes, como buscar intentos de inicio de sesión por usuario, dirección IP y estado de éxito. Las restricciones aseguran la integridad de los datos, evitando valores no permitidos en la columna de razón de fallo.
