## api.seed_document_type
**Proposito:** La función `api.seed_document_type` se encarga de procesar un array de tipos de documentos proporcionados en el payload `p_input`. Para cada tipo de documento, la función verifica su validez, busca si ya existe en la base de datos, y realiza las operaciones correspondientes (INSERT o UPDATE) en la tabla `shared.document_type`. La función también devuelve un resultado que incluye el estado de cada operación y estadísticas sobre los tipos de documentos procesados.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.seed_document_type_input | Objeto de entrada que contiene un array de tipos de documentos a procesar. |

**Retorna:** Un objeto `api.seed_document_type_result` que contiene el estado de la operación, estadísticas y detalles sobre cada tipo de documento procesado.

**Tablas que lee:** `shared.document_type`

**Tablas que modifica (INSERT/UPDATE/DELETE):** `shared.document_type`

**Funciones que invoca:** No invoca ninguna función externa.

**Logica paso a paso:**
1. Valida que el array de tipos de documentos no sea nulo ni vacío.
2. Itera sobre cada tipo de documento en el array.
3. Realiza validaciones individuales para cada campo del tipo de documento.
4. Busca si el tipo de documento ya existe en la base de datos.
5. Si el tipo de documento existe, realiza un UPDATE si hay cambios, o un SKIP si no hay cambios.
6. Si el tipo de documento no existe, realiza un INSERT.
7. Almacena el resultado de cada operación en un array.
8. Devuelve un resultado global que incluye estadísticas y detalles de cada operación.

**Errores y excepciones:** 
- `NULL_ITEMS_ARRAY`: El array de ítems es NULL.
- `NO_ITEMS_PROVIDED`: El array de ítems está vacío.
- `MISSING_CODE`: El campo `code` es obligatorio.
- `DUPLICATE_CODE_IN_BATCH`: El `code` aparece más de una vez en el mismo lote.
- `INVALID_RESTRICTION_TYPE`: El valor del campo `restriction_type` no es válido.
- `INVALID_ENTITY_TYPE`: El valor del campo `entity_type` no es válido.
- `INVALID_ALERT_DAYS`: El valor del campo `alert_days_before` debe ser mayor a 0.
- `MISSING_ALERT_DAYS`: El campo `alert_days_before` es obligatorio cuando `requires_expiry` es TRUE.
- `MISSING_NAME`: El campo `name` es obligatorio.
- `INTERNAL_ERROR`: Error interno inesperado.

**Observaciones:** La función utiliza `SECURITY DEFINER` para ejecutar operaciones en la base de datos. No utiliza SQL dinámico.
