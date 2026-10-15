## core_operations.route_control
**Tipo:** tabla  
**Proposito:** Almacena información sobre los controles de ruta, incluyendo la secuencia, tiempos mínimos y máximos, tolerancia, y si es obligatorio.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| control_id | integer | No | nextval('core_operations.route_control_control_id_seq'::regclass) | Identificador único del control de ruta. |
| route_id | integer | No | Por confirmar | Identificador de la ruta a la que pertenece el control. |
| sequence_number | integer | No | Por confirmar | Número de secuencia del control en la ruta. |
| min_time_minutes | integer | No | Por confirmar | Tiempo mínimo permitido para el control. |
| max_time_minutes | integer | No | Por confirmar | Tiempo máximo permitido para el control. |
| tolerance_minutes | integer | Sí | 2 | Tolerancia adicional permitida para el control. |
| is_mandatory | boolean | Sí | true | Indica si el control es obligatorio. |
| created_at | timestamp with time zone | Sí | now() | Fecha y hora de creación del control. |
| checkpoint_id | integer | No | Por confirmar | Identificador del punto de control asociado. |

**Clave primaria:** control_id

**Claves foraneas:**  
- route_id -> core_operations.route(route_id)  
- checkpoint_id -> core_operations.checkpoint(checkpoint_id)

**Indices y restricciones:**  
- chk_control_times: Verifica que max_time_minutes sea mayor o igual que min_time_minutes.  
- uq_control_route_checkpoint: Garanteza la unicidad de la combinación de route_id y checkpoint_id.  
- idx_control_route: Índice en route_id e is_mandatory.  
- idx_route_control_route_id: Índice en route_id.

**Triggers:**  
- Por confirmar

**Observaciones:**  
- La tabla no tiene restricciones adicionales ni triggers definidos en el SQL proporcionado.
