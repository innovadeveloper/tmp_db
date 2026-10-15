## hr.person_address
**Tipo:** tabla
**Proposito:** Almacena las direcciones asociadas a las personas.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| address_id | bigint | No | nextval('hr.person_address_address_id_seq'::regclass) | Identificador único de la dirección |
| person_id | integer | No | | Identificador de la persona a la que pertenece la dirección |
| address_type | character varying(20) | No | | Tipo de dirección (HOME, WORK, TEMPORARY) |
| address_line1 | text | No | | Línea 1 de la dirección |
| address_line2 | text | Sí | | Línea 2 de la dirección (opcional) |
| district | character varying(100) | Sí | | Distrito o barrio |
| city | character varying(100) | Sí | | Ciudad |
| state | character varying(100) | Sí | | Estado o provincia |
| postal_code | character varying(20) | Sí | | Código postal |
| country | character varying(50) | Sí | 'PE' | País, por defecto Perú |
| latitude | numeric(10,8) | Sí | | Latitud geográfica |
| longitude | numeric(11,8) | Sí | | Longitud geográfica |
| is_primary | boolean | Sí | false | Indica si es la dirección principal |
| is_active | boolean | Sí | true | Indica si la dirección está activa |
| created_at | timestamp with time zone | Sí | now() | Fecha y hora de creación |
| updated_at | timestamp with time zone | Sí | now() | Fecha y hora de última actualización |

**Clave primaria:** address_id

**Claves foraneas:** person_id -> hr.person.person_id

**Indices y restricciones:** 
- idx_person_address_person: Índice B-tree en (person_id, is_active)
- idx_person_address_primary: Índice único B-tree en (person_id) donde is_primary = true
- chk_person_address_type: Verifica que address_type sea uno de 'HOME', 'WORK' o 'TEMPORARY'

**Triggers:** No se especifican en el SQL proporcionado

**Particionado:** No se especifica en el SQL proporcionado

**Observaciones:** Ninguna
