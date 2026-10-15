## api.upsert_vehicle_owner
**Proposito:** Inserta o actualiza un propietario de vehículo en la base de datos. Si el propietario ya existe, se actualizan sus datos; si no existe, se crea uno nuevo.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.upsert_vehicle_owner_input | Objeto de entrada que contiene los datos del propietario de vehículo a insertar o actualizar. |

**Retorna:** Un objeto `api.upsert_vehicle_owner_result` que contiene el resultado de la operación, incluyendo el estado del propietario, si ya existía, si se sincronizó el nombre completo, y los detalles del propietario.

**Tablas que lee:** `fleet.vehicle_owner`, `hr.person`

**Tablas que modifica (INSERT/UPDATE/DELETE):** `fleet.vehicle_owner`

**Funciones que invoca:** `validate_tax_id`

**Logica paso a paso:**
1. **Validación de `tax_id`:** Se verifica que el `tax_id` sea numérico o alfanumérico con un formato correcto.
2. **Validación de `bank_account`:** Se verifica que el `bank_account` tenga un formato correcto.
3. **Rama UPDATE:** Si `vehicle_owner_id` no es `NULL`, se verifica si el propietario existe. Si existe, se resincroniza el nombre completo y el `tax_id` desde `hr.person` si se solicita, o si no se proporciona un `tax_id` explícito. Luego, se detectan los cambios y se actualiza el propietario si hay cambios.
4. **Rama INSERT:** Si `vehicle_owner_id` es `NULL`, se verifica que `person_id` no sea `NULL` y que la persona exista en `hr.person`. Si la persona ya es propietaria, se retorna el propietario existente. Si no, se inserta un nuevo propietario.
5. **Poblar resultado:** Se pobla el resultado con los detalles del propietario actualizado o insertado.

**Errores y excepciones:**
- `unique_violation`: Se maneja una violación de unicidad al intentar insertar un propietario con un `person_id` que ya existe. Se retorna el propietario existente.
- `OTHERS`: Se manejan otros errores internos, retornando un código de error y un mensaje de error.

**Observaciones:** La función es segura para definir (`SECURITY DEFINER`) y puede ejecutarse por cualquier usuario. No utiliza SQL dinámico.
