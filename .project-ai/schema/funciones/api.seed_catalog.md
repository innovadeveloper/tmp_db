## api.seed_catalog
**Proposito:** La función `api.seed_catalog` se encarga de insertar o actualizar elementos en la tabla `shared.catalog` basándose en los datos proporcionados en un array de entrada. Valida las categorías y maneja la inserción de elementos, contando cuántos se insertaron y cuántos se omitieron.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_inputs | api.seed_catalog_input[] | Un array de objetos de entrada que contienen la categoría y los elementos a insertar. |

**Retorna:** Un objeto `api.seed_catalog_result` que contiene el resultado general de la operación, incluyendo el número de categorías procesadas, elementos insertados y omitidos, y detalles por categoría.

**Tablas que lee:** `shared.catalog`

**Tablas que modifica (INSERT/UPDATE/DELETE):** `shared.catalog`

**Funciones que invoca:** No invoca ninguna función externa.

**Logica paso a paso:**
1. Inicializa variables para almacenar resultados y contadores.
2. Define una lista de categorías válidas.
3. Itera sobre cada lote de entrada.
4. Valida que la categoría sea válida.
5. Cuenta los elementos existentes antes de la inserción.
6. Inserta cada elemento con `ON CONFLICT DO NOTHING` para evitar duplicados.
7. Cuenta los elementos existentes después de la inserción para calcular los insertados y omitidos.
8. Actualiza los contadores y resultados de la categoría actual.
9. Continúa con la siguiente categoría.
10. Genera el resultado global y lo devuelve.

**Errores y excepciones:** 
- Si ocurre un error inesperado, la función captura la excepción y devuelve un código de error interno junto con el mensaje de error.

**Observaciones:** 
- La función utiliza `ON CONFLICT DO NOTHING` para evitar la inserción de duplicados, lo que puede mejorar el rendimiento.
- La función maneja errores generales y devuelve detalles sobre el procesamiento parcial si ocurre un error.
