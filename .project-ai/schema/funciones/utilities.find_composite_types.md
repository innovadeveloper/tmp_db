## utilities.find_composite_types
**Proposito:** Devuelve una lista de tipos compuestos (composite types) en un esquema específico o en todos los esquemas si no se especifica.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_schema | text | Esquema en el que se buscarán los tipos compuestos. Si es NULL, se buscarán en todos los esquemas. |

**Retorna:** Una tabla con las columnas `schema_name`, `type_name` y `description`, que contienen el nombre del esquema, el nombre del tipo compuesto y su descripción, respectivamente.

**Tablas que lee:** `pg_type`, `pg_namespace`.

**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla.

**Funciones que invoca:** `obj_description`.

**Logica paso a paso:**
1. Se seleccionan los tipos compuestos (`typtype = 'c'`) desde la tabla `pg_type`.
2. Se filtran los tipos compuestos que pertenecen a esquemas que no sean `pg_catalog` ni `information_schema`.
3. Si se proporciona un esquema (`p_schema`), se filtran los tipos compuestos que pertenecen a ese esquema específico.
4. Se ordenan los resultados por el nombre del esquema y el nombre del tipo compuesto.

**Errores y excepciones:** No hay errores específicos definidos. La función utiliza `obj_description`, que puede lanzar excepciones si no se puede obtener la descripción del objeto.

**Observaciones:** La función es segura para definir (`SECURITY DEFINER`), lo que significa que se ejecutará con los privilegios del propietario de la función, no del usuario que la invoca. No utiliza SQL dinámico.
