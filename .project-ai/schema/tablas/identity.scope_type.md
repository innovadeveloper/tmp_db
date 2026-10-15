## identity.scope_type
**Tipo:** tabla
**Proposito:** Almacena los tipos de scopes disponibles en el sistema.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| scope_type_id | smallint | NO | nextval('identity.scope_type_scope_type_id_seq'::regclass) | Identificador único del tipo de scope. |
| code | character varying(50) | NO | Ninguna | Código único que identifica el tipo de scope. |
| description | text | Sí | Ninguna | Descripción detallada del tipo de scope. |

**Clave primaria:** scope_type_id
**Claves foraneas:** Ninguna
**Indices y restricciones:** scope_type_code_key (UNIQUE)
**Triggers:** Ninguno
**Particionado:** Ninguno
**Observaciones:** Ninguna
