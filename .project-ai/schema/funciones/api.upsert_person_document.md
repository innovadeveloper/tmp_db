## api.upsert_person_document
**Proposito:** Inserta o actualiza un documento de persona en la base de datos, validando los datos y gestionando el estado del documento.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.upsert_person_document_input | Objeto de entrada con los datos del documento de persona a insertar o actualizar. |

**Retorna:** Un objeto `api.upsert_person_document_result` que contiene el resultado de la operación, incluyendo el ID del documento, el tipo de operación (INSERT o UPDATE), el estado del documento, y otros detalles.

**Tablas que lee:** 
- `hr.person`: Para verificar si la persona existe.
- `shared.document_type`: Para obtener información sobre el tipo de documento.
- `identity.user`: Para verificar si el verificador existe y está activo.

**Tablas que modifica (INSERT/UPDATE/DELETE):** 
- `hr.person_document`: Para insertar o actualizar el documento de persona.

**Funciones que invoca:** 
- No invoca ninguna función externa.

**Logica paso a paso:** 
1. Valida si la persona existe.
2. Valida si el tipo de documento existe y está activo.
3. Valida si la fecha de vencimiento es obligatoria según el tipo de documento.
4. Valida si el rango de fechas es coherente.
5. Valida si el estado del documento está dentro del dominio permitido.
6. Valida si el verificador existe si se proporcionó.
7. Calcula los días hasta vencimiento y determina si el documento está por vencer.
8. Realiza un UPSERT en la tabla `hr.person_document`.
9. Pobla el objeto de resultado con los detalles del documento y la operación realizada.

**Errores y excepciones:** 
- `PERSON_NOT_FOUND`: La persona no existe.
- `DOCUMENT_TYPE_NOT_FOUND`: El tipo de documento no existe o está inactivo.
- `EXPIRY_DATE_REQUIRED`: El tipo de documento requiere una fecha de vencimiento y no se proporcionó.
- `INVALID_DATE_RANGE`: La fecha de vencimiento no es posterior a la fecha de emisión.
- `INVALID_DOCUMENT_STATUS`: El estado del documento no es válido.
- `VERIFIER_NOT_FOUND`: El verificador no existe o está inactivo.
- `INTERNAL_ERROR`: Error interno inesperado.

**Observaciones:** 
- La función utiliza `SECURITY DEFINER` para ejecutarse con los privilegios del propietario de la función.
- La función maneja transacciones implícitas para asegurar la consistencia de los datos.
