## utilities.find_listen_process
**Proposito:** Devuelve una lista de procesos que están escuchando (LISTEN) en la base de datos PostgreSQL.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| Ninguno |

**Retorna:** Una tabla con los siguientes campos:
- `pid` (integer): Identificador del proceso.
- `usename` (text): Nombre del usuario que ejecuta el proceso.
- `application_name` (text): Nombre de la aplicación que ejecuta el proceso.
- `state` (text): Estado del proceso.
- `query` (text): Consulta que está ejecutando el proceso.

**Tablas que lee:** `pg_stat_activity`

**Tablas que modifica (INSERT/UPDATE/DELETE):** Ninguna

**Funciones que invoca:** Ninguna

**Logica paso a paso:**
1. Selecciona los campos `pid`, `usename`, `application_name`, `state`, y `query` de la vista `pg_stat_activity`.
2. Filtra los resultados para incluir solo las filas donde la columna `query` comienza con la cadena 'LISTEN'.

**Errores y excepciones:** Ninguno

**Observaciones:** La función no realiza ninguna operación que pueda tener implicaciones de seguridad o rendimiento significativas.
