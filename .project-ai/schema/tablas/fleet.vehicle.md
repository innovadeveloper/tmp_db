## fleet.vehicle
**Tipo:** tabla
**Proposito:** Almacena información detallada sobre los vehículos de la flota, incluyendo su identificación, detalles técnicos, estado y operatividad.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| vehicle_id | integer | No | Sí | Identificador único del vehículo. |
| plate_number | character varying(10) | No | Sí | Placa oficial del vehículo (ej: ABC-123). |
| internal_code | character varying(20) | No | Sí | Código interno de la empresa (ej: BUS-001). |
| company_id | integer | No | Sí | Identificador de la empresa a la que pertenece el vehículo. |
| brand | character varying(100) | Sí | Sí | Marca del vehículo. |
| model | character varying(100) | Sí | Sí | Modelo del vehículo. |
| year | integer | Sí | Sí | Año de fabricación del vehículo. |
| chassis_number | character varying(50) | Sí | Sí | Número de chasis del vehículo. |
| engine_number | character varying(50) | Sí | Sí | Número de motor del vehículo. |
| fuel_type | character varying(20) | Sí | Sí | Tipo de combustible del vehículo (DIESEL, GNV, HYBRID, ELECTRIC, GASOLINE). |
| seating_capacity | integer | Sí | Sí | Capacidad de asientos del vehículo. |
| standing_capacity | integer | Sí | Sí | Capacidad de pie del vehículo. |
| color | character varying(50) | Sí | Sí | Color del vehículo. |
| status | character varying(20) | No | 'ACTIVE' | Estado del vehículo (ACTIVE, INACTIVE, MAINTENANCE, RETIRED). |
| acquisition_date | date | Sí | Sí | Fecha de adquisición del vehículo. |
| is_operational | boolean | No | true | Indica si el vehículo está operativo. |
| created_at | timestamp with time zone | No | now() | Fecha y hora de creación del registro. |
| updated_at | timestamp with time zone | No | now() | Fecha y hora de última actualización del registro. |

**Clave primaria:** vehicle_id

**Claves foraneas:** company_id -> shared.company.company_id

**Indices y restricciones:** 
- chk_vehicle_capacity: Verifica que la capacidad de asientos y pie sean válidas.
- chk_vehicle_fuel_type: Verifica que el tipo de combustible sea uno de los permitidos.
- chk_vehicle_plate_format: Verifica que el formato de la placa sea válido.
- chk_vehicle_status: Verifica que el estado del vehículo sea uno de los permitidos.
- chk_vehicle_year: Verifica que el año de fabricación sea válido.
- vehicle_chassis_number_key: Único por número de chasis.
- vehicle_internal_code_key: Único por código interno.
- vehicle_plate_number_key: Único por placa.

**Triggers:** No se especifican en el SQL proporcionado.

**Observaciones:** 
- La columna `fuel_type` tiene un valor por defecto pero no se especifica en el SQL proporcionado.
- La columna `status` tiene un valor por defecto pero no se especifica en el SQL proporcionado.
- El índice `idx_vehicle_gps_operational` se refiere a una columna `is_operational` que no existe en la tabla proporcionada.
