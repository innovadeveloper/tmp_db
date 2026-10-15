## api.upsert_personnel
**Proposito:** La función `api.upsert_personnel` permite insertar o actualizar un registro de personal en la base de datos. Si se proporciona un `personnel_id`, intenta actualizar el registro existente. Si no se proporciona, intenta insertar un nuevo registro.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.upsert_personnel_input | Un objeto que contiene los datos del personal a insertar o actualizar. |

**Retorna:** Un objeto `api.upsert_personnel_result` que contiene el resultado de la operación, incluyendo el estado de éxito, cualquier error, el ID del personal, y otros detalles.

**Tablas que lee:** 
- `hr.personnel`
- `hr.person`
- `shared.catalog`
- `shared.configuration`
- `identity."user"`

**Tablas que modifica (INSERT/UPDATE/DELETE):** 
- `hr.personnel`

**Funciones que invoca:** 
- `api._generate_employee_code()`

**Logica paso a paso:** 
1. Si `personnel_id` no es `NULL`, intenta actualizar el registro existente.
2. Valida los campos proporcionados, incluyendo `job_title`, `employment_type`, `employment_status`, `hire_date`, `user_id`, y `employee_code`.
3. Si los campos son válidos, realiza la actualización o inserción.
4. Si ocurre un error de unicidad, devuelve un error de conflicto de unicidad.
5. Si ocurre cualquier otro error, devuelve un error interno.

**Errores y excepciones:** 
- `unique_violation`: Devuelve un error de conflicto de unicidad si ocurre.
- `OTHERS`: Devuelve un error interno con el mensaje de error.

**Observaciones:** 
- La función verifica la existencia de registros relacionados y valida los valores de entrada.
- Si el `employee_code` es `NULL` o vacío, genera uno automáticamente.
- La función maneja errores de validación y devuelve mensajes de error descriptivos.
- La función utiliza una transacción implícita para asegurar la consistencia de los datos.
