## api.log_login_attempt
**Proposito:** Registra un intento de inicio de sesión y realiza análisis de fuerza bruta basado en los intentos fallidos.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.log_login_attempt_input | Datos del intento de inicio de sesión a registrar. |

**Retorna:** api.log_login_attempt_result - Resultado del intento de inicio de sesión, incluyendo el nivel de riesgo de fuerza bruta.

**Tablas que lee:** identity.login_attempt

**Tablas que modifica (INSERT/UPDATE/DELETE):** identity.login_attempt

**Funciones que invoca:** Por confirmar

**Logica paso a paso:**
1. Valida que los parámetros `username`, `ip_address` y `success` no sean nulos.
2. Si `success` es `FALSE`, valida que `failure_reason` no sea nulo y esté dentro del dominio permitido.
3. Inserta el intento de inicio de sesión en la tabla `identity.login_attempt`.
4. Calcula el número de intentos fallidos del mismo `username` en los últimos 15 minutos y desde la misma `ip_address` en la última hora.
5. Determina el nivel de riesgo de fuerza bruta basado en los intentos fallidos.
6. Devuelve el resultado del intento de inicio de sesión, incluyendo el nivel de riesgo de fuerza bruta.

**Errores y excepciones:**
- `check_violation`: Si la constraint de la tabla `login_attempt` es violada (por ejemplo, `failure_reason` en un intento de inicio de sesión exitoso).
- `OTHERS`: Cualquier otro error inesperado.

**Observaciones:** La función utiliza `SECURITY DEFINER` para ejecutarse con los privilegios del propietario de la función.
