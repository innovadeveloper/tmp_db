## utilities.find_queue_usage
**Proposito:** Devuelve el uso actual de la cola de notificaciones de PostgreSQL.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| Ninguno |

**Retorna:** Un número que representa el uso actual de la cola de notificaciones.

**Tablas que lee:** `pg_stat_activity`

**Tablas que modifica (INSERT/UPDATE/DELETE):** Ninguna

**Funciones que invoca:** `pg_notification_queue_usage()`

**Logica paso a paso:**
1. La función invoca a `pg_notification_queue_usage()` para obtener el uso actual de la cola de notificaciones.

**Errores y excepciones:** No hay validaciones explícitas en el código proporcionado.

**Observaciones:** La función es simple y no realiza ninguna operación que pueda tener riesgos de seguridad o rendimiento significativos.
