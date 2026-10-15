## core_operations.route
**Tipo:** tabla  
**Proposito:** Almacena información sobre las rutas de transporte autorizadas por ATU.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| route_id | integer | No | Sí | Identificador único de la ruta. |
| company_id | integer | No | Sí | Identificador de la compañía que opera la ruta. |
| code | character varying(20) | No | Sí | Código único de la ruta. |
| name | character varying(255) | No | Sí | Nombre de la ruta. |
| route_type | character varying(20) | Sí | Sí | Tipo de ruta (LINEAR o CIRCULAR). |
| total_distance_km | numeric(8,2) | Sí | Sí | Distancia total de la ruta en kilómetros. |
| estimated_duration_minutes | integer | Sí | Sí | Duración estimada de la ruta en minutos. |
| is_active | boolean | Sí | true | Indica si la ruta está activa. |
| created_at | timestamp with time zone | Sí | now() | Fecha y hora de creación de la ruta. |
| updated_at | timestamp with time zone | Sí | now() | Fecha y hora de última actualización de la ruta. |

**Clave primaria:** route_id  
**Claves foraneas:** company_id -> shared.company.company_id  
**Indices y restricciones:**  
- uq_route_company_code: Único para cada combinación de company_id y code.  
- chk_route_type: Verifica que route_type sea NULL o uno de los valores 'LINEAR' o 'CIRCULAR'.  
- idx_route_code: Índice B-tree en la columna code.  
- idx_route_company: Índice B-tree en la columna company_id y is_active.

**Triggers:** No se especifican en el SQL proporcionado.

**Observaciones:**  
- La columna route_type tiene una restricción CHECK que permite valores NULL o 'LINEAR' y 'CIRCULAR'.
