## utilities.find_types_by_name
**Proposito:** Devuelve una lista de tipos de datos definidos en un esquema específico.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_schema | text | Esquema en el que se buscarán los tipos de datos. Si no se proporciona, se buscarán en todos los esquemas no estándar. |

**Retorna:** Una tabla con las siguientes columnas:
- schema_name: Nombre del esquema.
- type_name: Nombre del tipo de dato.
- description: Descripción del tipo de dato.

**Tablas que lee:** pg_type, pg_namespace.

**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla.

**Funciones que invoca:** obj_description.

**Logica paso a paso:**
1. Filtra los tipos de datos (`pg_type`) que son complejos (`typtype = 'c'`).
2. Excluye los esquemas estándar (`pg_catalog` y `information_schema`).
3. Si se proporciona un esquema (`p_schema`), filtra los tipos de datos que coinciden con el patrón proporcionado.
4. Devuelve una tabla con el nombre del esquema, el nombre del tipo de dato y su descripción.

**Errores y excepciones:** No hay validaciones explícitas en el código proporcionado.

**Observaciones:** La función utiliza `obj_description` para obtener la descripción del tipo de dato, lo que puede ser costoso en términos de rendimiento si se invoca con frecuencia. La función no es definida como `SECURITY DEFINER`, por lo que no tiene privilegios adicionales sobre las tablas que consulta.
