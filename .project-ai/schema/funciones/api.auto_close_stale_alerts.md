## api.auto_close_stale_alerts
**Proposito:** Cierra automáticamente alertas que han pasado el tiempo de cierre automático definido.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| Ninguno |

**Retorna:** `api.auto_close_stale_alerts_result`
**Tablas que lee:** `shared.configuration`, `core_operations.alert`
**Tablas que modifica (INSERT/UPDATE/DELETE):** `core_operations.alert`, `identity.activity_log`
**Funciones que invoca:** `NULL`
**Logica paso a paso:**
1. Lee el tamaño del lote (`batch_size`) desde la configuración.
2. Identifica las alertas que deben ser cerradas automáticamente (`status` en `ACTIVE` o `ACKNOWLEDGED`, `auto_closed_at` no nulo y expirado).
3. Cierra las alertas seleccionadas en lote.
4. Registra la ejecución del trabajo en `identity.activity_log`.
5. Pone los resultados en `api.auto_close_stale_alerts_result`.
**Errores y excepciones:** Registra errores en `identity.activity_log` y devuelve un resultado de error.
**Observaciones:** Utiliza un lote para evitar bloquear la tabla y registra la ejecución para trazabilidad.
