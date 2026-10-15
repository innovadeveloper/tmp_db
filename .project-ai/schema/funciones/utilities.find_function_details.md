## utilities.find_function_details
**Proposito:** Busca y devuelve detalles de funciones en el esquema que coinciden con un patrón de búsqueda.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_search | text | Patrón de búsqueda para el nombre de las funciones |

**Retorna:** Una tabla con detalles de las funciones que coinciden con el patrón de búsqueda.
- schema_name: Nombre del esquema donde se encuentra la función.
- function_name: Nombre de la función.
- arguments: Argumentos de entrada de la función.
- return_type: Tipo de retorno de la función.
- returns_table: Indica si la función retorna una tabla.
- definition: Definición completa de la función.

**Tablas que lee:** pg_proc, pg_namespace
**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla.
**Funciones que invoca:** pg_get_function_arguments, pg_get_function_result, pg_get_functiondef
**Logica paso a paso:**
1. Selecciona las funciones del esquema que no sean parte de 'pg_catalog' o 'information_schema'.
2. Filtra las funciones cuyos nombres coinciden con el patrón de búsqueda proporcionado.
3. Devuelve los detalles de las funciones que coinciden.
**Errores y excepciones:** No hay excepciones específicas definidas.
**Observaciones:** La función es segura para definidores (SECURITY DEFINER) y no utiliza SQL dinámico.
