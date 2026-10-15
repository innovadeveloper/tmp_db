## utilities.find_notification_queue_status
**Proposito:** Esta función devuelve el estado de la cola de notificaciones, indicando el uso de la cola y su condición (OK, WARNING o CRITICAL).

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| Ninguno |

**Retorna:** Una tabla con dos columnas: `usage` (número) y `status` (texto), que indican el uso de la cola y su estado respectivo.

**Tablas que lee:** `pg_notification_queue_usage()`

**Tablas que modifica (INSERT/UPDATE/DELETE):** Ninguna

**Funciones que invoca:** `pg_notification_queue_usage()`

**Logica paso a paso:**
1. Utiliza la función `pg_notification_queue_usage()` para obtener el uso actual de la cola de notificaciones.
2. Evalúa el uso de la cola y asigna un estado (`OK`, `WARNING`, `CRITICAL`) basado en el valor de uso.

**Errores y excepciones:** No se especifican excepciones en el código proporcionado.

**Observaciones:** La función no realiza ninguna operación que pueda afectar la seguridad o el rendimiento del sistema.
