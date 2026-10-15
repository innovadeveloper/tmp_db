## utilities.find_functions_by_schema
**Proposito:** Busca y devuelve una lista de funciones en un esquema específico, incluyendo su nombre, tipo de retorno y parámetros.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_schema | text | El nombre del esquema en el que se buscarán las funciones. |

**Retorna:** Una tabla con las siguientes columnas:
- schema_name: Nombre del esquema.
- function_name: Nombre de la función.
- return_type: Tipo de retorno de la función.
- parameters: Parámetros de la función.

**Tablas que lee:** pg_proc, pg_namespace.

**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla.

**Funciones que invoca:** pg_get_function_result, pg_get_function_arguments.

**Logica paso a paso:**
1. Selecciona el nombre del esquema, el nombre de la función, el tipo de retorno y los parámetros de las funciones.
2. Filtra las funciones basándose en el nombre del esquema proporcionado, utilizando una comparación insensible a mayúsculas y minúsculas.
3. Ordena los resultados por el nombre de la función.

**Errores y excepciones:** No se especifican excepciones en el código proporcionado.

**Observaciones:** La función utiliza una comparación insensible a mayúsculas y minúsculas para buscar el esquema, lo que permite una búsqueda parcial. No se especifica una cláusula WHERE para filtrar por el esquema, lo que significa que la función buscará en todos los esquemas que contengan el texto proporcionado en su nombre.
