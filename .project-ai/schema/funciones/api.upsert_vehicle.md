## api.upsert_vehicle
**Proposito:** Inserta o actualiza un vehículo en la base de datos, dependiendo si el `vehicle_id` proporcionado es `NULL` o no. Realiza validaciones y control de errores para garantizar la integridad de los datos.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.upsert_vehicle_input | Objeto de entrada que contiene los datos del vehículo a insertar o actualizar. |

**Retorna:** `api.upsert_vehicle_result` - Un objeto que indica el éxito o fracaso de la operación, el estado del vehículo (`INSERTED` o `UPDATED`), y detalles sobre el código interno generado.

**Tablas que lee:** 
- `fleet.vehicle` - Para verificar la existencia de un vehículo, validar la unicidad de placa, chasis y código interno, y obtener datos del vehículo existente.
- `shared.company` - Para validar la existencia y estado de la empresa asociada al vehículo.

**Tablas que modifica (INSERT/UPDATE/DELETE):** 
- `fleet.vehicle` - Para insertar un nuevo vehículo o actualizar los datos de uno existente.

**Funciones que invoca:** 
- `api._generate_vehicle_code()` - Genera un código interno único para el vehículo si no se proporciona uno.

**Logica paso a paso:** 
1. Si `vehicle_id` es `NULL`, valida y registra un nuevo vehículo.
2. Si `vehicle_id` no es `NULL`, valida y actualiza el vehículo existente.
3. Realiza validaciones de formato y unicidad para placa, chasis, código interno, tipo de combustible, estado, año, y capacidades.
4. Detecta cambios en los datos del vehículo y realiza la actualización si hay cambios.
5. Genera un código interno único si no se proporciona uno.
6. Registra el vehículo en la base de datos.
7. Devuelve el resultado de la operación.

**Errores y excepciones:** 
- `unique_violation`: Maneja conflictos de unicidad, como placa, chasis o código interno duplicados.
- `check_violation`: Maneja violaciones de constraint en la tabla `fleet.vehicle`.
- `OTHERS`: Maneja cualquier otro error inesperado.

**Observaciones:** 
- La función utiliza `SECURITY DEFINER` para permitir que los usuarios con privilegios ejecuten la función.
- La función maneja la generación de códigos interno únicos si no se proporciona uno.
- La función realiza validaciones exhaustivas para garantizar la integridad de los datos.
