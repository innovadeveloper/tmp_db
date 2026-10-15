## core_operations.alert_daily_summary
**Tipo:** tabla
**Proposito:** Almacena resúmenes diarios de alertas, incluyendo estadísticas y datos agregados.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| summary_id | bigint | No | nextval('core_operations.alert_daily_summary_summary_id_seq'::regclass) | Identificador único de cada resumen diario de alertas. |
| summary_date | date | No | Por confirmar | Fecha del resumen diario de alertas. |
| total_alerts | integer | Sí | 0 | Total de alertas registradas en el día. |
| critical_count | integer | Sí | 0 | Cantidad de alertas críticas. |
| high_count | integer | Sí | 0 | Cantidad de alertas de alto nivel. |
| medium_count | integer | Sí | 0 | Cantidad de alertas de nivel medio. |
| low_count | integer | Sí | 0 | Cantidad de alertas de nivel bajo. |
| active_count | integer | Sí | 0 | Cantidad de alertas activas. |
| acknowledged_count | integer | Sí | 0 | Cantidad de alertas reconocidas. |
| resolved_count | integer | Sí | 0 | Cantidad de alertas resueltas. |
| avg_acknowledgment_min | numeric(8,2) | Sí | 0 | Promedio de tiempo en minutos para reconocer las alertas. |
| avg_resolution_min | numeric(8,2) | Sí | 0 | Promedio de tiempo en minutos para resolver las alertas. |
| top_alert_types | jsonb | Sí | Por confirmar | Tipos de alertas más comunes en formato JSONB. |
| top_vehicles | jsonb | Sí | Por confirmar | Vehículos involucrados en las alertas más comunes en formato JSONB. |
| created_at | timestamp with time zone | Sí | now() | Fecha y hora de creación del resumen diario de alertas. |

**Clave primaria:** summary_id
**Claves foraneas:** Ninguna
**Indices y restricciones:** 
- `alert_daily_summary_summary_date_key`: Único para cada fecha de resumen diario.
**Triggers:** Ninguno
**Observaciones:** 
- La columna `summary_date` debería tener una restricción de no nulo para garantizar que cada resumen tenga una fecha asociada.
