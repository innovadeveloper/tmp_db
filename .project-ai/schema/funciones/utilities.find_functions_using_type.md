## utilities.find_functions_using_type
**Proposito:** Busca funciones que dependen de un tipo específico en la base de datos.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_type_name | text | Nombre del tipo de datos a buscar |

**Retorna:** Una tabla con la siguiente información:
- `usage_type`: Tipo de dependencia ('DEPENDENCY').
- `schema_name`: Nombre del esquema donde se encuentra la función.
- `function_name`: Nombre de la función.
- `return_type`: Tipo de retorno de la función.
- `parameters`: Parámetros de la función.

**Tablas que lee:** pg_type, pg_depend, pg_proc, pg_namespace.

**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla.

**Funciones que invoca:** pg_get_function_result, pg_get_function_arguments.

**Logica paso a paso:**
1. Busca en la tabla `pg_type` el tipo de datos que coincida con el nombre proporcionado.
2. Utiliza `pg_depend` para encontrar las dependencias de ese tipo.
3. Filtra las dependencias para obtener solo las que son funciones (`pg_proc`).
4. Obtiene el esquema, nombre, tipo de retorno y parámetros de las funciones dependientes.
5. Devuelve una tabla con la información de las funciones encontradas.

**Errores y excepciones:** No hay validaciones explícitas en el código proporcionado.

**Observaciones:** La función es segura para definir (`SECURITY DEFINER`) y no utiliza SQL dinámico.
