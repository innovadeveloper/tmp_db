## utilities.find_idle_in_transaction
**Proposito:** Devuelve una lista de procesos (pid) que están en estado 'idle in transaction' y que han estado inactivos durante un período de tiempo mayor a los minutos especificados.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_minutes | integer | Duración en minutos para considerar un proceso como inactivo. Valor por defecto es 5 minutos. |

**Retorna:** Una tabla con los siguientes campos:
- pid: Identificador del proceso.
- usename: Nombre del usuario que ejecuta el proceso.
- application_name: Nombre de la aplicación que ejecuta el proceso.
- state: Estado actual del proceso.
- state_change: Fecha y hora en que cambió el estado del proceso.
- idle_duration: Duración de inactividad del proceso.

**Tablas que lee:** pg_stat_activity

**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla.

**Funciones que invoca:** No invoca ninguna función.

**Logica paso a paso:**
1. Selecciona los procesos que están en estado 'idle in transaction'.
2. Filtra los procesos que han estado inactivos durante un período mayor a los minutos especificados.
3. Calcula la duración de inactividad del proceso.
4. Ordena los resultados por la fecha y hora en que cambió el estado del proceso.

**Errores y excepciones:** No hay errores o excepciones específicas definidas.

**Observaciones:** La función utiliza la vista pg_stat_activity para obtener información sobre los procesos en ejecución. No realiza ninguna operación que pueda afectar la seguridad o el rendimiento del sistema.
