## utilities.find_functions_returning_type
**Proposito:** Busca funciones en el esquema que devuelven un tipo específico.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_type_name | text | Nombre del tipo de dato que debe devolver la función |

**Retorna:** Una tabla con las siguientes columnas:
- schema_name: Nombre del esquema donde se encuentra la función
- function_name: Nombre de la función
- return_type: Tipo de dato que devuelve la función
- parameters: Parámetros de la función

**Tablas que lee:** pg_proc, pg_namespace

**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla

**Funciones que invoca:** pg_get_function_result, pg_get_function_arguments

**Logica paso a paso:**
1. Selecciona las funciones del sistema que devuelven un tipo similar al especificado.
2. Devuelve una tabla con el esquema, nombre, tipo de retorno y parámetros de las funciones encontradas.

**Errores y excepciones:** No lanza errores específicos, pero puede devolver resultados vacíos si no se encuentran funciones que coincidan con el tipo especificado.

**Observaciones:** La búsqueda es insensible a mayúsculas y minúsculas gracias al uso de ILIKE.
