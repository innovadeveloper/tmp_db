## public.flyway_schema_history
**Tipo:** tabla
**Proposito:** Almacena el historial de migraciones de esquema ejecutadas por Flyway.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| installed_rank | integer | No | Ninguna | Rango de instalación de la migración. |
| version | character varying(50) | No | Ninguna | Versión de la migración. |
| description | character varying(200) | No | Ninguna | Descripción de la migración. |
| type | character varying(20) | No | Ninguna | Tipo de migración (por ejemplo, 'SQL'). |
| script | character varying(1000) | No | Ninguna | Nombre del archivo de script de migración. |
| checksum | integer | Sí | Ninguna | Suma de verificación del script de migración. |
| installed_by | character varying(100) | No | Ninguna | Usuario que instaló la migración. |
| installed_on | timestamp without time zone | No | now() | Fecha y hora de instalación de la migración. |
| execution_time | integer | No | Ninguna | Tiempo de ejecución de la migración en milisegundos. |
| success | boolean | No | Ninguna | Indica si la migración fue exitosa. |

**Clave primaria:** installed_rank

**Claves foraneas:** Ninguna

**Indices y restricciones:** 
- flyway_schema_history_s_idx: Índice B-tree en la columna success.

**Triggers:** Ninguna

**Particionado:** Ninguna

**Observaciones:** Ninguna
