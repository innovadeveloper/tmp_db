## api.get_document_types
**Proposito:** Obtiene los tipos de documentos según los filtros proporcionados.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.get_document_types_input_v2 | Objeto de entrada con los filtros para la consulta. |

**Retorna:** Un objeto `api.get_document_types_result_v2` que contiene los tipos de documentos que cumplen con los filtros, junto con información de filtrado y conteo.

**Tablas que lee:** `shared.document_type`

**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla.

**Funciones que invoca:** No invoca ninguna función externa.

**Logica paso a paso:**
1. Normaliza los filtros proporcionados en `p_input`.
2. Valida los valores de `entity_type` y `restriction_type` si se proporcionan.
3. Ejecuta una consulta SQL para obtener los tipos de documentos que cumplen con los filtros.
4. Pone los resultados en el objeto de resultado `v_result`.
5. Maneja cualquier excepción que pueda ocurrir durante la ejecución.

**Errores y excepciones:** 
- `INVALID_ENTITY_TYPE`: Si `entity_type` no es uno de los valores permitidos.
- `INVALID_RESTRICTION_TYPE`: Si `restriction_type` no es uno de los valores permitidos.
- `INTERNAL_ERROR`: Para cualquier otra excepción inesperada.

**Observaciones:** La función utiliza `COALESCE` y `NULLIF` para manejar los valores nulos y vacíos en los filtros. No realiza ninguna operación que pueda modificar las tablas de la base de datos.
