## identity.login_attempt_2026_06
**Tipo:** tabla
**Proposito:** Almacena intentos de inicio de sesión del sistema, incluyendo detalles sobre el usuario, la dirección IP, el agente del usuario, el resultado del intento y la razón de falla.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| attempt_id | bigint | No | nextval('identity.login_attempt_attempt_id_seq'::regclass) | Identificador único del intento de inicio de sesión. |
| username | character varying(100) | No | Por confirmar | Nombre de usuario que intentó iniciar sesión. |
| ip_address | inet | No | Por confirmar | Dirección IP desde la que se intentó iniciar sesión. |
| user_agent | text | Sí | Por confirmar | Información sobre el agente del usuario que intentó iniciar sesión. |
| success | boolean | No | Por confirmar | Indica si el intento de inicio de sesión fue exitoso o no. |
| failure_reason | character varying(100) | Sí | Por confirmar | Razón por la que el intento de inicio de sesión falló. Solo se registra si `success` es `false`. |
| attempted_at | timestamp with time zone | No | now() | Fecha y hora en que se intentó iniciar sesión. |

**Clave primaria:** attempt_id, attempted_at
**Claves foraneas:** Ninguna
**Indices y restricciones:** 
- chk_login_failure_reason: Asegura que si el intento fue exitoso, la razón de falla no debe estar definida.
- chk_login_failure_values: Asegura que la razón de falla solo puede tomar uno de los valores predefinidos si el intento fue fallido.
- login_attempt_2026_06_ip_address_attempted_at_idx: Índice en ip_address y attempted_at para mejorar la eficiencia de las consultas filtradas por dirección IP y fecha.
- login_attempt_2026_06_ip_address_attempted_at_idx1: Índice adicional para mejorar la eficiencia de las consultas filtradas por dirección IP, fecha y resultado de éxito.
- login_attempt_2026_06_success_attempted_at_idx: Índice en success y attempted_at para mejorar la eficiencia de las consultas filtradas por resultado de éxito y fecha.
- login_attempt_2026_06_username_attempted_at_idx: Índice en username y attempted_at para mejorar la eficiencia de las consultas filtradas por nombre de usuario y fecha.
- login_attempt_2026_06_username_attempted_at_idx1: Índice adicional para mejorar la eficiencia de las consultas filtradas por nombre de usuario, fecha y resultado de éxito.

**Triggers:** Por confirmar
**Particionado:** Por confirmar
**Observaciones:** La tabla incluye índices para mejorar la eficiencia de las consultas, pero no se especifican las particiones o triggers.
