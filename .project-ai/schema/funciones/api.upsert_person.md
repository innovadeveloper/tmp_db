## api.upsert_person
**Proposito:** Inserta o actualiza una persona en la base de datos, dependiendo si se proporciona un `person_id` o no. Valida los datos de entrada y maneja casos de duplicidad de `tax_id`.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.upsert_person_input | Objeto que contiene los datos de la persona a insertar o actualizar. |

**Retorna:** Un objeto `api.upsert_person_result` que indica el éxito o fracaso de la operación, el estado de la persona (`INSERTED` o `UPDATED`), y los detalles de la persona.

**Tablas que lee:** `hr.person`
**Tablas que modifica (INSERT/UPDATE/DELETE):** `hr.person`
**Funciones que invoca:** `validate_tax_id` (subfunción local)
**Logica paso a paso:**
1. Valida el `tax_id_type` y formato.
2. Valida el género, estado civil y fecha de nacimiento.
3. Si `person_id` es `NULL`, valida que el `tax_id` no exista ya.
4. Calcula el `full_name`.
5. Si `person_id` es `NULL`, inserta la persona. Si no, actualiza la persona si hay cambios.
6. Devuelve los detalles de la persona insertada o actualizada.

**Errores y excepciones:**
- `INVALID_TAX_ID_TYPE`: El `tax_id_type` es inválido.
- `INVALID_TAX_ID_FORMAT`: El formato del `tax_id` es inválido.
- `INVALID_GENDER`: El género es inválido.
- `INVALID_MARITAL_STATUS`: El estado civil es inválido.
- `INVALID_BIRTH_DATE`: La fecha de nacimiento es inválida.
- `INVALID_EMAIL_FORMAT`: El formato del email es inválido.
- `PERSON_NOT_FOUND`: El `person_id` no existe.
- `MISSING_GIVEN_NAMES`: El `given_names` es obligatorio.
- `MISSING_FATHER_LAST_NAME`: El `father_last_name` es obligatorio.
- `MISSING_MOTHER_LAST_NAME`: El `mother_last_name` es obligatorio.
- `MISSING_TAX_ID`: El `tax_id` es obligatorio al crear una persona.
- `DUPLICATE_TAX_ID`: El `tax_id` ya está registrado para otra persona.
- `INTERNAL_ERROR`: Error interno inesperado.

**Observaciones:** La función maneja casos de duplicidad de `tax_id` mediante una excepción `unique_violation`. La validación de `tax_id` se realiza en una subfunción local para evitar duplicidad. La función es segura contra inyección SQL debido a su uso de parámetros de entrada.
