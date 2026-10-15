## fleet.vehicle_assignment
**Tipo:** tabla
**Proposito:** Almacena el historial de asignaciones de conductores a vehículos, incluyendo detalles sobre el tipo de asignación, fechas de asignación y desasignación, y el estado de la asignación.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| assignment_id | bigint | No | Sí | Identificador único de la asignación |
| vehicle_id | integer | No | Sí | Identificador del vehículo asignado |
| driver_id | integer | No | Sí | Identificador del conductor asignado |
| assigned_at | timestamp with time zone | Sí | now() | Fecha y hora en que se realizó la asignación |
| unassigned_at | timestamp with time zone | Sí | Sí | Fecha y hora en que se desasignó el vehículo; NULL indica que la asignación está activa |
| assignment_type | character varying(20) | Sí | 'REGULAR' | Tipo de asignación (OWNER_OPERATOR, HIRED_DRIVER, TEMPORARY, REPLACEMENT) |
| assigned_by | bigint | No | Sí | Identificador del usuario que realizó la asignación |
| unassigned_by | bigint | Sí | Sí | Identificador del usuario que desasignó el vehículo |
| notes | text | Sí | Sí | Notas adicionales sobre la asignación |
| is_active | boolean | Sí | true | Indica si la asignación está activa |
| created_at | timestamp with time zone | Sí | now() | Fecha y hora en que se creó la asignación |

**Clave primaria:** assignment_id

**Claves foraneas:** 
- driver_id -> hr.driver.driver_id
- assigned_by -> identity."user".user_id
- unassigned_by -> identity."user".user_id
- vehicle_id -> fleet.vehicle.vehicle_id

**Indices y restricciones:** 
- chk_vehicle_assignment_dates: Verifica que la fecha de desasignación sea posterior a la de asignación
- chk_vehicle_assignment_type: Verifica que el tipo de asignación sea uno de los permitidos
- idx_vehicle_assignment_active_unique: Índice único para vehículos activos
- idx_vehicle_assignment_dates: Índice por fecha de asignación y desasignación
- idx_vehicle_assignment_driver: Índice por conductor y estado de asignación
- idx_vehicle_assignment_type: Índice por tipo de asignación y estado de asignación
- idx_vehicle_assignment_vehicle: Índice por vehículo y estado de asignación

**Triggers:** No se especifican triggers en el SQL proporcionado.

**Observaciones:** 
- La columna `driver_id` tiene un comentario que indica que se creará una restricción de clave foranea en un archivo separado.
- La columna `unassigned_at` tiene un comentario que indica que NULL significa que la asignación está activa.
- La columna `assignment_type` tiene un comentario que lista los tipos de asignación permitidos.
