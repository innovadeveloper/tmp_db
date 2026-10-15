## fleet.vehicle_owner
**Tipo:** tabla
**Proposito:** Almacena información sobre los propietarios de vehículos (owner-operators).

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| vehicle_owner_id | integer | No | nextval('fleet.vehicle_owner_vehicle_owner_id_seq'::regclass) | Identificador único del propietario de vehículo. |
| person_id | integer | No | Por confirmar | Identificador del individuo que es propietario del vehículo (FK a hr.person). |
| tax_id | character varying(20) | Sí | Ninguno | Identificación fiscal del propietario. |
| full_name | character varying(255) | No | Ninguno | Nombre completo del propietario. |
| email | character varying(255) | Sí | Ninguno | Correo electrónico del propietario. |
| phone | character varying(50) | Sí | Ninguno | Número de teléfono del propietario. |
| address | text | Sí | Ninguno | Dirección del propietario. |
| bank_account | character varying(50) | Sí | Ninguno | Cuenta bancaria para liquidaciones. |
| is_active | boolean | Sí | true | Indica si el propietario está activo. |
| created_at | timestamp with time zone | Sí | now() | Fecha y hora de creación del registro. |
| updated_at | timestamp with time zone | Sí | now() | Fecha y hora de la última actualización del registro. |

**Clave primaria:** vehicle_owner_id

**Claves foraneas:** person_id -> hr.person.person_id

**Indices y restricciones:** 
- idx_vehicle_owner_name_trgm: Índice GIN para búsqueda por nombre utilizando trigramas.
- idx_vehicle_owner_person: Índice B-tree para person_id.
- idx_vehicle_owner_tax_id: Índice B-tree para tax_id, filtrado por is_active = true.
- fk_vehicle_owner_person: Restricción de clave foránea que restringe la eliminación de registros en hr.person si existen registros relacionados en fleet.vehicle_owner.

**Triggers:** No se especifican en el SQL proporcionado.

**Particionado:** No se especifica en el SQL proporcionado.

**Observaciones:** Ninguna.
