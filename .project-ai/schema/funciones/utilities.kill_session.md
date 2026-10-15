## utilities.kill_session
**Proposito:** Termina una sesión de PostgreSQL identificada por su PID.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_pid | integer | Identificador único de la sesión a terminar |

**Retorna:** Un booleano que indica si la sesión fue terminada con éxito.

**Tablas que lee:** No lee ninguna tabla.

**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla.

**Funciones que invoca:** No invoca ninguna función.

**Logica paso a paso:**
1. Intenta terminar la sesión de PostgreSQL con el PID proporcionado utilizando la función `pg_terminate_backend`.
2. Almacena el resultado de la operación en la variable `v_result`.
3. Devuelve el valor de `v_result`.

**Errores y excepciones:** No hay validaciones explícitas. Si el PID no corresponde a ninguna sesión activa, `pg_terminate_backend` devolverá `false`.

**Observaciones:** La función debe ser ejecutada por un usuario con privilegios adecuados para terminar sesiones de PostgreSQL.
