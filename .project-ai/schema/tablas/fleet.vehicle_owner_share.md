## fleet.vehicle_owner_share
**Tipo:** tabla
**Proposito:** Almacena la participación de los propietarios en vehículos compartidos, incluyendo el porcentaje de propiedad y las fechas de validez.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| share_id | integer | No | Sí | Identificador único de la participación |
| vehicle_id | integer | No | Sí | Identificador del vehículo |
| vehicle_owner_id | integer | No | Sí | Identificador del propietario |
| ownership_percentage | numeric(5,2) | No | Sí | Porcentaje de propiedad del vehículo |
| valid_from | date | No | Sí | Fecha de inicio de validez de la participación |
| valid_until | date | Sí | Sí | Fecha de fin de validez de la participación |
| is_active | boolean | Sí | true | Indica si la participación está activa |
| created_at | timestamp with time zone | Sí | now() | Fecha y hora de creación |
| updated_at | timestamp with time zone | Sí | now() | Fecha y hora de última actualización |

**Clave primaria:** share_id
**Claves foraneas:** vehicle_owner_id -> fleet.vehicle_owner.vehicle_owner_id, vehicle_id -> fleet.vehicle.vehicle_id
**Indices y restricciones:** chk_vehicle_share_dates, chk_vehicle_share_percentage, uq_vehicle_owner_period, idx_vehicle_share_active, idx_vehicle_share_owner, idx_vehicle_share_vehicle
**Triggers:** Por confirmar
**Particionado:** Por confirmar
**Observaciones:** La suma de ownership_percentage por vehicle_id debe ser 100%.
