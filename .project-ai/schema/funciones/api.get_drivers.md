## api.get_drivers
**Proposito:** Obtiene una lista paginada de conductores que cumplen con ciertos criterios de filtro.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.get_drivers_input | Objeto de entrada que contiene los criterios de filtro y paginación |

**Retorna:** Un objeto `api.get_drivers_result` que contiene la lista de conductores, información de paginación y filtros aplicados.

**Tablas que lee:** 
- `hr.driver`
- `hr.person`
- `shared.company`
- `fleet.vehicle`
- `hr.person_document`
- `shared.document_type`

**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla.

**Funciones que invoca:** No invoca ninguna función externa.

**Logica paso a paso:**
1. Normaliza los parámetros de entrada, incluyendo la paginación y los filtros.
2. Realiza validaciones en los filtros de estado de empleo, tipo de empleo y compañía.
3. Cuenta el total de conductores que cumplen con los filtros.
4. Realiza la consulta principal para obtener los conductores paginados, incluyendo detalles del vehículo y documentos críticos vencidos.
5. Construye el resultado final con la lista de conductores, información de paginación y filtros aplicados.

**Errores y excepciones:** 
- Si ocurre un error interno, devuelve un código de error `INTERNAL_ERROR` y el mensaje de error.

**Observaciones:** 
- La función utiliza una consulta con CTE (Common Table Expressions) para optimizar el rendimiento al dividir la consulta en pasos.
- La función no modifica ninguna tabla, solo realiza consultas de lectura.
- La función utiliza funciones de validación para asegurar que los filtros sean válidos.
