## core_operations.alert_type
**Tipo:** tabla  
**Proposito:** Almacena información sobre los tipos de alertas que pueden ocurrir en el sistema.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| alert_type_id | integer | No | nextval('core_operations.alert_type_alert_type_id_seq'::regclass) | Identificador único del tipo de alerta. |
| code | character varying(50) | No | Por confirmar | Código único para identificar el tipo de alerta. |
| name | character varying(100) | No | Por confirmar | Nombre descriptivo del tipo de alerta. |
| description | text | Sí | Por confirmar | Descripción detallada del tipo de alerta. |
| category | character varying(50) | Sí | Por confirmar | Categoría a la que pertenece el tipo de alerta. |
| severity | character varying(20) | No | 'INFO' | Gravedad del tipo de alerta, debe ser uno de 'CRITICAL', 'HIGH', 'MEDIUM', 'LOW' o 'INFO'. |
| requires_acknowledgment | boolean | Sí | false | Indica si el tipo de alerta requiere una confirmación. |
| auto_close_after_min | integer | Sí | Por confirmar | Tiempo en minutos después del cual la alerta se cierra automáticamente. |
| notification_channels | text[] | Sí | Por confirmar | Lista de canales de notificación asociados al tipo de alerta. |
| display_order | integer | Sí | 0 | Orden de visualización del tipo de alerta. |
| is_active | boolean | Sí | true | Indica si el tipo de alerta está activo. |
| created_at | timestamp with time zone | Sí | now() | Fecha y hora en que se creó el tipo de alerta. |

**Clave primaria:** alert_type_id  
**Claves foraneas:** Ninguna  
**Indices y restricciones:**  
- alert_type_code_key: Único para el código del tipo de alerta.
- chk_alert_type_severity: Verifica que la gravedad del tipo de alerta sea uno de los valores permitidos.

**Triggers:**  
- Por confirmar

**Observaciones:**  
- La columna `code` debe ser única para evitar duplicados.
- La columna `severity` tiene una restricción de verificación para permitir solo valores específicos.
- La columna `auto_close_after_min` y `notification_channels` pueden requerir validaciones adicionales según las necesidades del sistema.
