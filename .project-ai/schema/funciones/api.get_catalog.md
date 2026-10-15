## api.get_catalog
**Proposito:** La función `api.get_catalog` se utiliza para leer un catálogo genérico agrupado por categoría. Permite filtrar por categorías específicas y controlar si solo se devuelven los elementos activos.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_categories | character varying[] | Array de categorías a filtrar. Si es `NULL`, se devuelven todas las categorías. |
| p_only_active | boolean | Indica si solo se deben devolver los elementos activos. El valor por defecto es `TRUE`. |

**Retorna:** Un resultado de tipo `api.get_catalog_result` que contiene información sobre el catálogo, incluyendo el número total de categorías y elementos, y los elementos agrupados por categoría.

**Tablas que lee:** `shared.catalog`

**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla.

**Funciones que invoca:** No invoca ninguna función externa.

**Logica paso a paso:**
1. **Validación de categorías:** Si se proporciona un array de categorías, se valida que todas sean conocidas. Si alguna categoría es desconocida, se devuelve un error.
2. **Consulta principal:** Se realiza una consulta para obtener los elementos del catálogo, filtrando por las categorías y actividad según los parámetros proporcionados.
3. **Agrupamiento:** Los resultados se agrupan por categoría.
4. **Conteo y normalización:** Se cuentan el número total de categorías y elementos, y se normalizan los resultados para evitar `NULL` cuando no hay filas.
5. **Retorno:** Se devuelve el resultado en el formato `api.get_catalog_result`.

**Errores y excepciones:** Se capturan excepciones generales y se devuelve un error interno con el mensaje de error correspondiente.

**Observaciones:** La función utiliza índices específicos según el valor de `p_only_active` para optimizar el rendimiento. No modifica ninguna tabla y no invoca funciones externas.
