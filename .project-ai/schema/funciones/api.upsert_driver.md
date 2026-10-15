## api.upsert_driver
**Proposito:** Inserta o actualiza un conductor en la base de datos. Maneja tanto la creación de nuevos conductores como la actualización de conductores existentes, incluyendo la validación de datos y la gestión de relaciones con otras tablas.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.upsert_driver_input | Objeto de entrada que contiene los datos del conductor a insertar o actualizar. |

**Retorna:** Un objeto `api.upsert_driver_result` que contiene el resultado de la operación, incluyendo el estado de éxito, mensajes de error, y detalles del conductor.

**Tablas que lee:** 
- `hr.driver`
- `hr.person`
- `fleet.vehicle_owner`
- `identity."user"`
- `shared.company`

**Tablas que modifica (INSERT/UPDATE/DELETE):** 
- `hr.driver`
- `hr.person`

**Funciones que invoca:** 
- `api.upsert_person`

**Logica paso a paso:**
1. **Validación y recuperación de datos existentes:**
   - Si `driver_id` es proporcionado, verifica si el conductor existe.
   - Si `person_data` está presente, intenta actualizar la persona asociada.

2. **Validaciones de negocio:**
   - Verifica que el `employment_type` y `employment_status` sean válidos.
   - Asegura que el `owner_id` y `hired_by_owner_id` sean válidos si el `employment_type` es `OWNER_OPERATOR` o `HIRED_DRIVER`.
   - Verifica que el `driver_code` no esté duplicado.
   - Asegura que el `user_id` no esté vinculado a otro conductor.

3. **Procesamiento de datos:**
   - Si `driver_id` es `NULL`, intenta crear un nuevo conductor.
   - Si `person_id` es `NULL`, intenta crear una nueva persona.
   - Genera un `driver_code` si no se proporciona uno.

4. **Ejecución de la operación:**
   - Si se detectan cambios, actualiza el conductor.
   - Si no hay cambios, marca la operación como `SKIPPED`.
   - Si no se detectan cambios, inserta un nuevo conductor.

5. **Retorno del resultado:**
   - Llena el objeto de resultado con los detalles del conductor y los estados de éxito o error.

**Errores y excepciones:**
- `unique_violation`: Maneja conflictos de unicidad, como duplicados en `driver_code`.
- `OTHERS`: Maneja cualquier otra excepción inesperada.

**Observaciones:** 
- La función utiliza `SECURITY DEFINER` para ejecutar operaciones como `INSERT` y `UPDATE` en tablas que requieren privilegios adicionales.
- La función maneja la creación y actualización de relaciones entre tablas, asegurando la integridad de los datos.
