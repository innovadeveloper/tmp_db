## hr.person
**Tipo:** tabla
**Proposito:** Tabla base universal de personas que contiene información detallada sobre los individuos, incluyendo datos personales, contacto y estado de actividad.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| person_id | integer | No | Sí | Identificador único de la persona. |
| tax_id | character varying(20) | No | Sí | Documento de identidad de la persona. |
| full_name | character varying(255) | No | Sí | Nombre completo de la persona. |
| gender | character varying(1) | Sí | Sí | Genero de la persona (M, F, O). |
| birth_date | date | Sí | Sí | Fecha de nacimiento de la persona. |
| nationality | character varying(50) | Sí | Sí | Nacionalidad de la persona. |
| marital_status | character varying(20) | Sí | Sí | Estado civil de la persona (SINGLE, MARRIED, DIVORCED, WIDOWED). |
| blood_type | character varying(5) | Sí | Sí | Tipo sanguíneo de la persona. |
| email | character varying(255) | Sí | Sí | Correo electrónico de la persona. |
| phone_mobile | character varying(20) | Sí | Sí | Número de teléfono móvil de la persona. |
| phone_home | character varying(20) | Sí | Sí | Número de teléfono fijo de la persona. |
| emergency_contact_name | character varying(255) | Sí | Sí | Nombre del contacto de emergencia de la persona. |
| emergency_contact_phone | character varying(20) | Sí | Sí | Número de teléfono del contacto de emergencia de la persona. |
| photo_url | character varying(500) | Sí | Sí | URL de la foto de la persona. |
| is_active | boolean | No | true | Indica si la persona está activa. |
| created_at | timestamp with time zone | No | now() | Fecha y hora de creación de la persona. |
| updated_at | timestamp with time zone | No | now() | Fecha y hora de última actualización de la persona. |
| given_names | character varying(150) | No | Sí | Nombres de pila de la persona. |
| father_last_name | character varying(100) | No | Sí | Apellido paterno de la persona. |
| mother_last_name | character varying(100) | No | Sí | Apellido materno de la persona. |

**Clave primaria:** person_id
**Claves foraneas:** Ninguna
**Indices y restricciones:** 
- chk_person_gender: Valida el género de la persona.
- chk_person_marital_status: Valida el estado civil de la persona.
- person_pkey: Clave primaria de la tabla.
- person_tax_id_key: Clave única por tax_id.
- idx_person_active: Índice por is_active.
- idx_person_full_name: Índice por full_name.
- idx_person_full_name_trgm: Índice GIN por full_name para búsqueda trigramática.
- idx_person_tax_id: Índice por tax_id.
- idx_person_tax_id_trgm: Índice GIN por tax_id para búsqueda trigramática.
**Triggers:** Por confirmar
**Particionado:** Por confirmar
**Observaciones:** La tabla incluye campos para datos personales, contacto y estado de actividad, con restricciones de validación para el género y el estado civil. También cuenta con índices para mejorar el rendimiento en consultas frecuentes.
