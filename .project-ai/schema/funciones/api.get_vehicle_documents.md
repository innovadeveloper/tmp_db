## api.get_vehicle_documents
**Proposito:** Obtiene los documentos de un vehículo, filtrados por estado y tipo de restricción, y devuelve información detallada sobre el vehículo y sus documentos.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.get_vehicle_documents_input | Objeto de entrada que contiene los parámetros para la consulta, incluyendo el identificador del vehículo o su placa, y filtros para el estado y tipo de restricción de los documentos. |

**Retorna:** Un objeto `api.get_vehicle_documents_result` que contiene la información del vehículo y sus documentos, incluyendo estadísticas y detalles de los documentos.

**Tablas que lee:** 
- `fleet.vehicle`
- `shared.company`
- `fleet.vehicle_document`
- `shared.document_type`
- `identity."user"`

**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla.

**Funciones que invoca:** No invoca ninguna función externa.

**Logica paso a paso:**
1. Valida que se proporcione exactamente un identificador de vehículo (o placa).
2. Resuelve el identificador de vehículo si se proporciona una placa.
3. Valida los filtros de estado y tipo de restricción.
4. Realiza una consulta principal que:
   - Obtiene los datos del vehículo y la empresa asociada.
   - Obtiene los documentos del vehículo, aplicando los filtros de estado y tipo de restricción.
   - Calcula estadísticas sobre los documentos.
5. Devuelve los resultados en un objeto `api.get_vehicle_documents_result`.

**Errores y excepciones:** 
- `MISSING_VEHICLE_IDENTIFIER`: Se proporciona ni `vehicle_id` ni `plate_number`.
- `AMBIGUOUS_VEHICLE_IDENTIFIER`: Se proporcionan ambos `vehicle_id` y `plate_number`.
- `VEHICLE_NOT_FOUND`: El vehículo no existe.
- `INVALID_STATUS`: El estado proporcionado no es válido.
- `INVALID_RESTRICTION_TYPE`: El tipo de restricción proporcionado no es válido.
- `INTERNAL_ERROR`: Error interno inesperado.

**Observaciones:** 
- La función utiliza un solo CTE para optimizar el rendimiento.
- La función no modifica ninguna tabla.
- La función utiliza validaciones y filtros para asegurar la integridad de los datos.
