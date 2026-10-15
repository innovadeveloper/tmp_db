## core_operations.incident_type
**Tipo:** tabla  
**Proposito:** Almacena información sobre los tipos de incidentes que pueden ocurrir en el sistema.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| incident_type_id | integer | No | Sí | Identificador único del tipo de incidente. |
| code | character varying(50) | No | Sí | Código único para identificar el tipo de incidente. |
| name | character varying(100) | No | Sí | Nombre descriptivo del tipo de incidente. |
| description | text | Sí | Sí | Descripción detallada del tipo de incidente. |
| category | character varying(50) | Sí | Sí | Categoría a la que pertenece el tipo de incidente. |
| default_severity | character varying(20) | No | Sí | Severidad predeterminada para este tipo de incidente. |
| requires_report | boolean | No | Falso | Indica si este tipo de incidente requiere un informe. |
| notify_authorities | boolean | No | Falso | Indica si este tipo de incidente requiere la notificación de autoridades. |
| is_active | boolean | No | Verdadero | Indica si este tipo de incidente está activo y puede ser utilizado. |
| created_at | timestamp with time zone | No | Ahora | Fecha y hora en que se creó el tipo de incidente. |

**Clave primaria:** incident_type_id  
**Claves foraneas:** Ninguna  
**Indices y restricciones:** incident_type_code_key (UNIQUE)  
**Triggers:** Ninguno  
**Observaciones:** Ninguna
