## utilities.find_idle_listeners
**Proposito:** Devuelve una lista de conexiones inactivas en la base de datos que están escuchando (LISTEN).

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| Ninguno |

**Retorna:** Una tabla con las siguientes columnas:
- `pid`: Identificador del proceso de la conexión.
- `usename`: Nombre del usuario que inició la conexión.
- `application_name`: Nombre del cliente que inició la conexión.
- `state`: Estado de la conexión.
- `query`: Consulta actual en ejecución.
- `idle_time`: Tiempo inactivo de la conexión.

**Tablas que lee:** `pg_stat_activity`

**Tablas que modifica (INSERT/UPDATE/DELETE):** Ninguna

**Funciones que invoca:** Ninguna

**Logica paso a paso:**
1. Selecciona las columnas `pid`, `usename`, `application_name`, `state`, `query` y el tiempo inactivo (`now() - state_change`) de las conexiones en `pg_stat_activity`.
2. Filtra las conexiones donde la consulta (`query`) comienza con 'LISTEN' y el estado (`state`) es 'idle'.

**Errores y excepciones:** Ninguno

**Observaciones:** La función no realiza ninguna modificación en la base de datos ni invoca otras funciones. Es una consulta simple que filtra y selecciona información de la vista `pg_stat_activity`.
