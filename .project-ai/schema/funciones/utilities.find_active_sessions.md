## utilities.find_active_sessions
**Proposito:** Devuelve información sobre las sesiones activas en el servidor PostgreSQL, excluyendo la sesión actual.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| Ninguno |

**Retorna:** Una tabla con las siguientes columnas:
- `pid`: Identificador del proceso de la sesión.
- `usename`: Nombre del usuario que inició la sesión.
- `application_name`: Nombre de la aplicación que inició la sesión.
- `state`: Estado actual de la sesión.
- `wait_event_type`: Tipo de evento de espera.
- `wait_event`: Evento de espera.
- `time_in_state`: Tiempo que la sesión ha estado en su estado actual.
- `query`: Consulta actual que se está ejecutando en la sesión.

**Tablas que lee:** `pg_stat_activity`

**Tablas que modifica (INSERT/UPDATE/DELETE):** Ninguna

**Funciones que invoca:** Ninguna

**Logica paso a paso:**
1. Selecciona las columnas especificadas de la vista `pg_stat_activity`.
2. Filtra las sesiones donde `backend_type` es 'client backend' y `pid` no es el de la sesión actual (`pg_backend_pid()`).

**Errores y excepciones:** No hay validaciones explícitas en el código.

**Observaciones:** La función no realiza ninguna operación que pueda tener implicaciones de rendimiento significativas o seguridad. No es una función `SECURITY DEFINER`. No utiliza SQL dinámico.
