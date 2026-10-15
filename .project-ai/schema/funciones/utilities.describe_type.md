## utilities.describe_type
**Proposito:** Devuelve una descripción de las columnas de un tipo de datos específico en PostgreSQL.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_type_name | text | Nombre del tipo de datos para el que se desea obtener la descripción |

**Retorna:** Una tabla con las siguientes columnas:
- column_name: Nombre de la columna
- data_type: Tipo de datos de la columna
- position_at: Posición de la columna en el tipo de datos
- is_array: Indica si la columna es un array

**Tablas que lee:** pg_attribute, pg_type

**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla

**Funciones que invoca:** pg_catalog.format_type

**Logica paso a paso:**
1. Recibe el nombre de un tipo de datos como parámetro.
2. Realiza una consulta a las tablas pg_attribute y pg_type para obtener información sobre las columnas del tipo de datos especificado.
3. Filtra las columnas para incluir solo las que no están marcadas como eliminadas (attisdropped) y que tienen un número de atributo mayor que 0.
4. Formatea el tipo de datos y determina si es un array.
5. Devuelve una tabla con la información de las columnas.

**Errores y excepciones:** No hay validaciones explícitas en el código proporcionado.

**Observaciones:** La función utiliza funciones del sistema de PostgreSQL para obtener información sobre los tipos de datos y sus columnas. No realiza modificaciones en la base de datos ni invoca otras funciones complejas.
