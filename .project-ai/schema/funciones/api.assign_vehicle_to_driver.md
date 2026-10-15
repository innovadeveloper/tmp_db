## api.assign_vehicle_to_driver
**Proposito:** Asigna un vehículo a un conductor y registra la asignación.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.assign_vehicle_to_driver_input | Datos de entrada para la asignación del vehículo al conductor. |

**Retorna:** api.assign_vehicle_to_driver_result
**Tablas que lee:** fleet.vehicle, hr.driver, hr.person, fleet.vehicle_assignment, identity.user
**Tablas que modifica (INSERT/UPDATE/DELETE):** fleet.vehicle_assignment, hr.driver
**Funciones que invoca:** Por confirmar
**Logica paso a paso:**
1. Valida el tipo de asignación.
2. Valida que el usuario que realiza la asignación exista y esté activo.
3. Valida que el vehículo exista y esté en estado activo y operacional.
4. Valida que el conductor exista y esté activo y disponible.
5. Cierra la asignación previa del vehículo si existe.
6. Inserta la nueva asignación del vehículo al conductor.
7. Actualiza el vehículo del conductor.
8. Pobla el resultado con los datos de la asignación.
**Errores y excepciones:** 
- INVALID_ASSIGNMENT_TYPE: El tipo de asignación no es válido.
- GRANTING_USER_NOT_FOUND: El usuario que realiza la asignación no existe o está inactivo.
- VEHICLE_NOT_FOUND: El vehículo no existe.
- VEHICLE_NOT_ACTIVE: El vehículo no está en estado activo.
- VEHICLE_NOT_OPERATIONAL: El vehículo no está operacional.
- DRIVER_NOT_FOUND: El conductor no existe.
- DRIVER_NOT_ACTIVE: El conductor no está activo.
- DRIVER_NOT_AVAILABLE: El conductor no está disponible.
- INTERNAL_ERROR: Error interno inesperado.
**Observaciones:** La función es segura para definir (SECURITY DEFINER) y maneja transacciones internas.
