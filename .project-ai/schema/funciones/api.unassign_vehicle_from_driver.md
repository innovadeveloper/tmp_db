## api.unassign_vehicle_from_driver
**Proposito:** Desasigna un vehículo de un conductor y registra la acción.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.unassign_vehicle_from_driver_input | Objeto de entrada con los detalles de la desasignación. |

**Retorna:** api.unassign_vehicle_from_driver_result
**Tablas que lee:** fleet.vehicle_assignment, fleet.vehicle, hr.driver, hr.person
**Tablas que modifica (INSERT/UPDATE/DELETE):** fleet.vehicle_assignment, hr.driver
**Funciones que invoca:** Por confirmar
**Logica paso a paso:**
1. Valida que el usuario que realiza la desasignación exista y esté activo.
2. Valida que el vehículo exista.
3. Valida que el conductor exista.
4. Valida que exista una asignación activa para el par vehículo-conductor.
5. Cierra la asignación actualizando la fecha de desasignación y el usuario que la realizó.
6. Limpia el `current_vehicle_id` del conductor.
7. Pobla el resultado con los detalles de la desasignación.
**Errores y excepciones:** 
- `UNASSIGNING_USER_NOT_FOUND`: El usuario que realiza la desasignación no existe o está inactivo.
- `VEHICLE_NOT_FOUND`: El vehículo no existe.
- `DRIVER_NOT_FOUND`: El conductor no existe.
- `NO_ACTIVE_ASSIGNMENT`: No existe una asignación activa para el par vehículo-conductor.
- `INTERNAL_ERROR`: Error interno inesperado.
**Observaciones:** La función es segura para definir (`SECURITY DEFINER`) y maneja excepciones para errores internos.
