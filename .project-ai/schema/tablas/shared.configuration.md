## shared.configuration
**Tipo:** tabla
**Proposito:** Almacena configuraciones globales del sistema, incluyendo su clave, valor, tipo de datos, descripción, editable o no, y timestamps de creación y actualización.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| config_id | integer | No | nextval('shared.configuration_config_id_seq'::regclass) | Identificador único de la configuración |
| key | character varying(100) | No | Por confirmar | Clave única que identifica la configuración, formato: module.section.parameter |
| value | text | No | Por confirmar | Valor de la configuración |
| data_type | character varying(20) | Sí | 'STRING' | Tipo de datos de la configuración (STRING, INTEGER, BOOLEAN, JSON, DECIMAL) |
| description | text | Sí | Por confirmar | Descripción de la configuración |
| is_editable | boolean | Sí | true | Indica si la configuración es editable |
| created_at | timestamp with time zone | Sí | now() | Fecha y hora de creación de la configuración |
| updated_at | timestamp with time zone | Sí | now() | Fecha y hora de la última actualización de la configuración |

**Clave primaria:** config_id
**Claves foraneas:** Ninguna
**Indices y restricciones:** 
- chk_config_data_type: Verifica que el tipo de datos sea uno de los permitidos (STRING, INTEGER, BOOLEAN, JSON, DECIMAL)
- configuration_key_key: Índice único en la columna key
- configuration_pkey: Clave primaria en la columna config_id
- idx_configuration_editable: Índice en la columna is_editable
- idx_configuration_key: Índice en la columna key
- idx_configuration_key_prefix: Índice en la columna key con soporte para operaciones de patrón de texto

**Triggers:** Por confirmar

**Particionado:** Por confirmar

**Observaciones:** 
- La columna 'key' tiene un formato específico que debe seguir (module.section.parameter), pero no se especifica el formato exacto en el diccionario de datos.
- La columna 'value' es de tipo text, lo que significa que puede almacenar cualquier tipo de dato, pero se recomienda seguir el tipo de datos especificado en 'data_type'.
- La columna 'is_editable' permite configuraciones críticas que no se pueden editar, lo cual puede ser útil para evitar cambios accidentales en configuraciones importantes.
- El uso de índices en 'is_editable', 'key' y 'key_prefix' puede mejorar el rendimiento de consultas que filtren o busquen por estas columnas.
