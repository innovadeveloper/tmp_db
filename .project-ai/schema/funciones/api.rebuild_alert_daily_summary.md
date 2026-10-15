## api.rebuild_alert_daily_summary
**Proposito:** Genera un resumen diario de alertas y lo almacena en la tabla `alert_daily_summary`. El resumen incluye el número de alertas por severidad, estado, tiempos promedio de reconocimiento y resolución, y los tipos de alerta y vehículos más comunes. La función es idempotente y puede re-ejecutarse para corregir errores.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_date | date | Fecha para la cual se genera el resumen. Por defecto es el día anterior. |

**Retorna:** Un objeto `api.rebuild_alert_daily_summary_result` que contiene el resultado de la operación, incluyendo el éxito, código de error, mensaje de error, fecha del resumen, operación realizada (INSERT o UPDATE) y el número total de alertas.

**Tablas que lee:** `core_operations.alert`

**Tablas que modifica (INSERT/UPDATE/DELETE):** `core_operations.alert_daily_summary`

**Funciones que invoca:** `None`

**Logica paso a paso:**
1. Determina la fecha a procesar, utilizando la fecha proporcionada o el día anterior si no se especifica.
2. Valida que la fecha no sea hoy o futura, devolviendo un error si es así.
3. Calcula los contadores de alertas por severidad y estado.
4. Calcula los tiempos promedio de reconocimiento y resolución.
5. Determina los tipos de alerta y vehículos más comunes.
6. Inserta o actualiza el resumen diario en la tabla `alert_daily_summary` utilizando un upsert idempotente.
7. Devuelve el resultado de la operación.

**Errores y excepciones:** 
- `INVALID_DATE`: Si la fecha proporcionada es hoy o futura.
- `INTERNAL_ERROR`: Para cualquier otro error inesperado.

**Observaciones:** La función es idempotente gracias al uso de `ON CONFLICT (summary_date) DO UPDATE`. Si no hay alertas para el día, inserta el registro en ceros para mantener la serie histórica. La función puede re-ejecutarse para corregir errores.
