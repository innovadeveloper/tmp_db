## utilities.find_terminate_backend
**Proposito:** Termina una conexión de backend PostgreSQL identificada por su PID, excepto la propia conexión que la ejecuta.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_pid | integer | Identificador del proceso backend que se desea terminar |

**Retorna:** boolean - Indica si la operación de terminación fue exitosa.

**Tablas que lee:** Por confirmar

**Tablas que modifica (INSERT/UPDATE/DELETE):** Por confirmar

**Funciones que invoca:** pg_terminate_backend, pg_backend_pid

**Logica paso a paso:**
1. Verifica si el PID proporcionado es el mismo que el PID de la conexión actual.
2. Si es el mismo, lanza una excepción indicando que no se puede terminar la propia conexión.
3. Si es diferente, invoca a pg_terminate_backend para terminar la conexión especificada.

**Errores y excepciones:** 
- Lanza una excepción si se intenta terminar la propia conexión.

**Observaciones:** La función debe ser ejecutada por un usuario con privilegios adecuados para terminar conexiones backend.
