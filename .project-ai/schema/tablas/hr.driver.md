## hr.driver
**Tipo:** tabla
**Proposito:** Almacena información sobre los conductores autorizados, incluyendo detalles sobre su empleo, licencia y disponibilidad.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| driver_id | integer | No | Sí | Identificador único del conductor |
| person_id | integer | No | Sí | Identificador de la persona asociada al conductor |
| user_id | bigint | Sí | Sí | Identificador del usuario asociado al conductor |
| company_id | integer | No | Sí | Identificador de la empresa a la que pertenece el conductor |
| driver_code | character varying(20) | No | Sí | Código único del conductor |
| hire_date | date | Sí | Sí | Fecha en que el conductor fue contratado |
| termination_date | date | Sí | Sí | Fecha en que el conductor fue terminado |
| employment_status | character varying(20) | Sí | 'ACTIVE' | Estado de empleo del conductor (ACTIVE, SUSPENDED, TERMINATED) |
| employment_type | character varying(20) | No | Sí | Tipo de empleo del conductor (OWNER_OPERATOR, HIRED_DRIVER) |
| owner_id | integer | Sí | Sí | Identificador del dueño del conductor |
| hired_by_owner_id | integer | Sí | Sí | Identificador del dueño que contrató al conductor |
| current_vehicle_id | integer | Sí | Sí | Identificador del vehículo actualmente asignado al conductor |
| license_points | integer | Sí | 100 | Puntos de licencia del conductor (rango 0-100) |
| total_trips | integer | Sí | 0 | Cantidad total de viajes realizados por el conductor |
| total_km_driven | numeric(12,2) | Sí | 0 | Kilómetros totales conducidos por el conductor |
| rating_average | numeric(3,2) | Sí | Sí | Promedio de calificaciones del conductor |
| is_available | boolean | Sí | true | Indica si el conductor está disponible para despacho |
| notes | text | Sí | Sí | Notas adicionales sobre el conductor |
| created_at | timestamp with time zone | Sí | now() | Fecha y hora de creación del registro |
| updated_at | timestamp with time zone | Sí | now() | Fecha y hora de última actualización del registro |

**Clave primaria:** driver_id
**Claves foraneas:** 
- person_id -> hr.person(person_id)
- user_id -> identity."user"(user_id)
- company_id -> shared.company(company_id)
- owner_id -> fleet.vehicle_owner(vehicle_owner_id)
- hired_by_owner_id -> fleet.vehicle_owner(vehicle_owner_id)
- current_vehicle_id -> fleet.vehicle(vehicle_id)
**Indices y restricciones:** 
- chk_driver_license_points: license_points >= 0 AND license_points <= 100
- chk_driver_status: employment_status = 'ACTIVE' OR employment_status = 'SUSPENDED' OR employment_status = 'TERMINATED'
- chk_driver_type: employment_type = 'OWNER_OPERATOR' OR employment_type = 'HIRED_DRIVER'
- driver_driver_code_key: UNIQUE (driver_code)
- driver_person_id_key: UNIQUE (person_id)
- driver_user_id_key: UNIQUE (user_id)
- idx_driver_available: B-tree (is_available, employment_status) WHERE is_available = true
- idx_driver_code: B-tree (driver_code)
- idx_driver_company: B-tree (company_id, employment_status)
- idx_driver_person: B-tree (person_id)
- idx_driver_vehicle: B-tree (current_vehicle_id) WHERE current_vehicle_id IS NOT NULL
**Triggers:** No se especifican en el SQL proporcionado
**Particionado:** No se especifica en el SQL proporcionado
**Observaciones:** No se identificaron problemas de diseño evidentes.
