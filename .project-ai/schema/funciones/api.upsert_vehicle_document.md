## api.upsert_vehicle_document
**Proposito:** Inserta o actualiza un documento de vehículo en la base de datos, realizando validaciones y actualizando el estado del vehículo si es necesario.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.upsert_vehicle_document_input | Objeto de entrada que contiene los datos del documento de vehículo a insertar o actualizar. |

**Retorna:** Un objeto `api.upsert_vehicle_document_result` que contiene el resultado de la operación, incluyendo el ID del documento de vehículo, la operación realizada (INSERTED o UPDATED), el código y nombre del tipo de documento, y otros detalles relevantes.

**Tablas que lee:** 
- `fleet.vehicle`
- `shared.document_type`
- `fleet.vehicle_document`
- `identity.user`

**Tablas que modifica (INSERT/UPDATE/DELETE):** 
- `fleet.vehicle_document`

**Funciones que invoca:** 
- `NULL`

**Logica paso a paso:** 
1. Valida si el vehículo existe.
2. Valida si el tipo de documento existe y está activo.
3. Valida si la fecha de vencimiento es requerida y si el rango de fechas es coherente.
4. Valida si el estado del documento está dentro del dominio permitido.
5. Valida si el verificador existe y está activo.
6. Determina si el documento ha expirado automáticamente.
7. Calcula los días hasta la expiración y establece el flag `expiring_soon`.
8. Realiza el UPSERT en la tabla `fleet.vehicle_document`.
9. Bloquea el vehículo automáticamente si el documento es crítico y ha expirado.
10. Pobla el resultado con los detalles del documento de vehículo y el estado del vehículo.

**Errores y excepciones:** 
- `VEHICLE_NOT_FOUND`: El vehículo no existe.
- `DOCUMENT_TYPE_NOT_FOUND`: El tipo de documento no existe.
- `DOCUMENT_TYPE_INACTIVE`: El tipo de documento está inactivo.
- `EXPIRY_DATE_REQUIRED`: El tipo de documento requiere una fecha de vencimiento.
- `INVALID_DATE_RANGE`: La fecha de vencimiento no es posterior a la fecha de emisión.
- `INVALID_DOCUMENT_STATUS`: El estado del documento no es válido.
- `VERIFIER_NOT_FOUND`: El verificador no existe o está inactivo.
- `INTERNAL_ERROR`: Error interno inesperado.

**Observaciones:** 
- La función utiliza `SECURITY DEFINER` para ejecutar operaciones como `UPDATE` en la tabla `fleet.vehicle`.
- La función maneja excepciones generales con `WHEN OTHERS THEN` y devuelve un error interno.
