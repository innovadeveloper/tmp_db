## api.upsert_companies
**Proposito:** La función `api.upsert_companies` inserta o actualiza registros de compañías en la base de datos. Recibe un array de objetos de entrada y devuelve un resultado que incluye detalles sobre los registros procesados, incluyendo inserciones, actualizaciones, saltos y errores.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.upsert_companies_input | Objeto de entrada que contiene un array de objetos de compañía a procesar. |

**Retorna:** Un objeto `api.upsert_companies_result` que contiene detalles sobre los registros procesados.

**Tablas que lee:** `shared.company`

**Tablas que modifica (INSERT/UPDATE/DELETE):** `shared.company`

**Funciones que invoca:** No invoca ninguna función externa.

**Logica paso a paso:** 
1. Valida que el array de compañías no sea nulo ni vacío.
2. Itera sobre cada compañía en el array.
3. Para cada compañía, verifica si es una inserción o una actualización basándose en el valor de `company_id`.
4. Realiza las validaciones necesarias (duplicidad, formato, etc.) según la operación (INSERT o UPDATE).
5. Si las validaciones son exitosas, realiza la operación (INSERT o UPDATE) y registra el resultado.
6. Al final, devuelve un objeto de resultado que incluye detalles sobre los registros procesados.

**Errores y excepciones:** 
- `NULL_COMPANIES_ARRAY`: El array de compañías es NULL.
- `NO_COMPANIES_PROVIDED`: El array de compañías está vacío.
- `DUPLICATE_COMPANY_ID_IN_BATCH`: `company_id` aparece más de una vez en el mismo lote.
- `COMPANY_NOT_FOUND`: La compañía con `company_id` especificado no existe.
- `INVALID_TAX_ID_FORMAT`: El formato del `tax_id` no es válido.
- `DUPLICATE_TAX_ID`: El `tax_id` ya está registrado en otra compañía.
- `MISSING_LEGAL_NAME`: El `legal_name` es obligatorio y no puede ser una cadena vacía.
- `MISSING_TAX_ID`: El `tax_id` es obligatorio al crear una compañía.
- `INTERNAL_ERROR`: Error interno inesperado.

**Observaciones:** La función utiliza `SECURITY DEFINER` para ejecutar operaciones en el nombre del rol que define la función. No utiliza SQL dinámico.
