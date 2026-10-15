## api.get_vehicles
**Proposito:** Obtiene una lista de vehículos filtrados según los criterios proporcionados, incluyendo información detallada sobre los propietarios y documentos asociados.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.get_vehicles_input | Objeto de entrada que contiene los criterios de filtro y paginación |

**Retorna:** Un objeto `api.get_vehicles_result` que contiene la lista de vehículos, la paginación, y los filtros aplicados.

**Tablas que lee:** 
- `fleet.vehicle`
- `shared.company`
- `fleet.vehicle_owner_share`
- `fleet.vehicle_owner`
- `fleet.vehicle_document`
- `shared.document_type`

**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla.

**Funciones que invoca:** No invoca ninguna función externa.

**Logica paso a paso:**
1. Normaliza los parámetros de entrada, incluyendo la paginación y los filtros.
2. Realiza validaciones sobre los filtros proporcionados.
3. Cuenta el total de vehículos que cumplen con los filtros.
4. Realiza la consulta principal para obtener los vehículos paginados.
5. Agrega información adicional sobre los propietarios y documentos de cada vehículo.
6. Construye el resultado final y lo devuelve.

**Errores y excepciones:** 
- Si ocurre un error inesperado, se captura y se devuelve un código de error `INTERNAL_ERROR` junto con el mensaje de error.

**Observaciones:** 
- La función utiliza `SECURITY DEFINER` para ejecutarse con los privilegios del propietario de la función.
- La consulta utiliza `LEFT JOIN` para asegurar que todos los vehículos, incluso sin propietarios o documentos, sean incluidos en el resultado.
- La función utiliza `array_agg` para construir el tipo compuesto `api.vehicle_list_item` sin conflictos de `GROUP BY`.
