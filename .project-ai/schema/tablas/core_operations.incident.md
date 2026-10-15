## core_operations.incident
**Tipo:** tabla  
**Proposito:** Almacena información sobre incidentes ocurridos en el sistema, incluyendo detalles sobre el tipo de incidente, vehículo, conductor, ruta, ubicación, gravedad, descripción, reporte y resolución del incidente.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| incident_id | bigint | No | Sí | Identificador único del incidente. |
| incident_type_id | integer | No | No | Identificador del tipo de incidente. |
| trip_id | bigint | Sí | No | Identificador del viaje asociado al incidente. |
| vehicle_id | integer | No | No | Identificador del vehículo involucrado en el incidente. |
| driver_id | integer | Sí | No | Identificador del conductor involucrado en el incidente. |
| route_id | integer | Sí | No | Identificador de la ruta en la que ocurrió el incidente. |
| incident_timestamp | timestamp with time zone | No | No | Fecha y hora en que ocurrió el incidente. |
| latitude | numeric(10,8) | Sí | No | Latitud de la ubicación del incidente. |
| longitude | numeric(11,8) | Sí | No | Longitud de la ubicación del incidente. |
| severity | character varying(20) | No | No | Gravedad del incidente (CRITICAL, HIGH, MEDIUM, LOW). |
| description | text | No | No | Descripción detallada del incidente. |
| reported_by | bigint | No | No | Identificador del usuario que reportó el incidente. |
| reported_at | timestamp with time zone | Sí | Sí | Fecha y hora en que el incidente fue reportado (por defecto la fecha actual). |
| resolved_by | bigint | Sí | No | Identificador del usuario que resolvió el incidente. |
| resolved_at | timestamp with time zone | Sí | No | Fecha y hora en que el incidente fue resuelto. |
| resolution_notes | text | Sí | No | Notas adicionales sobre la resolución del incidente. |
| status | character varying(20) | No | Sí | Estado actual del incidente (OPEN, IN_PROGRESS, RESOLVED, CLOSED). |
| created_at | timestamp with time zone | Sí | Sí | Fecha y hora en que el incidente fue creado (por defecto la fecha actual). |
| updated_at | timestamp with time zone | Sí | Sí | Fecha y hora en que el incidente fue actualizado (por defecto la fecha actual). |

**Clave primaria:** incident_id  
**Claves foraneas:**  
- driver_id -> hr.driver.driver_id  
- reported_by -> identity."user".user_id  
- resolved_by -> identity."user".user_id  
- route_id -> core_operations.route.route_id  
- incident_type_id -> core_operations.incident_type.incident_type_id  
- vehicle_id -> fleet.vehicle.vehicle_id  

**Indices y restricciones:**  
- chk_incident_severity: Verifica que la gravedad del incidente sea una de las permitidas (CRITICAL, HIGH, MEDIUM, LOW).  
- chk_incident_status: Verifica que el estado del incidente sea uno de los permitidos (OPEN, IN_PROGRESS, RESOLVED, CLOSED).  
- idx_incident_status: Índice B-tree en status y incident_timestamp para mejorar la búsqueda por estado y fecha.  
- idx_incident_time: Índice B-tree en incident_timestamp para mejorar la búsqueda por fecha.  
- idx_incident_vehicle: Índice B-tree en vehicle_id y incident_timestamp para mejorar la búsqueda por vehículo y fecha.  

**Triggers:**  
Por confirmar.  

**Observaciones:**  
- La columna trip_id es opcional y puede ser nula.  
- La columna driver_id es opcional y puede ser nula.  
- La columna reported_by es obligatoria y no puede ser nula.  
- La columna resolved_by es opcional y puede ser nula.  
- La columna severity tiene un valor por defecto 'OPEN'.  
- La columna status tiene un valor por defecto 'OPEN'.  
- La columna created_at y updated_at tienen valores por defecto la fecha actual.
