## utilities.find_functions_with_type_parameter
**Proposito:** Busca y devuelve una lista de funciones que contienen un parámetro del tipo especificado.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_type_name | text | Nombre del tipo de parámetro a buscar |

**Retorna:** Una tabla con las siguientes columnas:
- schema_name: Nombre del esquema donde se encuentra la función.
- function_name: Nombre de la función.
- parameters: Lista de parámetros de la función.
- return_type: Tipo de retorno de la función.

**Tablas que lee:** pg_proc, pg_namespace

**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla.

**Funciones que invoca:** pg_get_function_arguments, pg_get_function_result

**Logica paso a paso:**
1. Selecciona las funciones del sistema que contienen el tipo de parámetro especificado.
2. Devuelve una tabla con el esquema, nombre de la función, parámetros y tipo de retorno.

**Errores y excepciones:** No hay errores específicos definidos.

**Observaciones:** La función es segura para definir (SECURITY DEFINER) y no utiliza SQL dinámico.
