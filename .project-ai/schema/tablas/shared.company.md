## shared.company
**Tipo:** tabla
**Proposito:** Tabla que almacena información sobre las empresas operadoras. Cada fila representa una empresa con detalles como su identificación fiscal, nombre legal, nombre comercial, dirección, contacto y estado de activación.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| company_id | integer | No | nextval('shared.company_company_id_seq'::regclass) | Identificador único de la empresa. |
| tax_id | character varying(20) | No | | Identificación fiscal de la empresa (RUC en Perú). Debe ser un número de 11 dígitos. |
| legal_name | character varying(255) | No | | Nombre legal de la empresa. |
| trade_name | character varying(255) | Sí | | Nombre comercial usado en la interfaz de usuario. |
| address | text | Sí | | Dirección de la empresa. |
| phone | character varying(50) | Sí | | Número de teléfono de la empresa. |
| email | character varying(255) | Sí | | Correo electrónico de la empresa. |
| logo_url | character varying(500) | Sí | | URL del logotipo de la empresa. |
| is_active | boolean | No | true | Indica si la empresa está activa o no. |
| created_at | timestamp with time zone | No | now() | Fecha y hora de creación de la empresa. |
| updated_at | timestamp with time zone | No | now() | Fecha y hora de la última actualización de la empresa. |

**Clave primaria:** company_id
**Claves foraneas:** Ninguna
**Indices y restricciones:** 
- chk_company_tax_id_format: Verifica que el tax_id sea un número de 11 dígitos.
- company_pkey: Clave primaria de la tabla.
- company_tax_id_key: Índice único en tax_id para evitar duplicados.
- idx_company_legal_name_trgm: Índice GIN para búsqueda por trigramas en el nombre legal.
- idx_company_tax_id: Índice B-tree en tax_id para búsqueda rápida.

**Triggers:** Ninguno

**Particionado:** Ninguno

**Observaciones:** Ninguna
