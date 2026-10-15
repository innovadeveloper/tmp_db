## identity.user
**Tipo:** tabla
**Proposito:** Almacena información de los usuarios del sistema vinculados a LDAP/WSO2, incluyendo detalles de autenticación externa y estado de cuenta.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| user_id | bigint | No | nextval('identity.user_user_id_seq'::regclass) | Identificador único del usuario. |
| external_id | character varying(255) | No | Por confirmar | Identificador externo del usuario, como LDAP DN o UUID desde WSO2. |
| username | character varying(100) | No | Por confirmar | Nombre de usuario único dentro del sistema. |
| email | character varying(255) | No | Por confirmar | Email del usuario, almacenado para mejorar el rendimiento. |
| full_name | character varying(255) | Sí | Por confirmar | Nombre completo del usuario. |
| is_active | boolean | Sí | true | Indica si el usuario está activo. |
| last_login_at | timestamp with time zone | Sí | Por confirmar | Fecha y hora de la última sesión del usuario. |
| created_at | timestamp with time zone | Sí | now() | Fecha y hora de creación del registro del usuario. |
| updated_at | timestamp with time zone | Sí | now() | Fecha y hora de la última actualización del registro del usuario. |

**Clave primaria:** user_id
**Claves foraneas:** Ninguna
**Indices y restricciones:** 
- user_email_key: Único por email
- user_external_id_key: Único por external_id
- user_pkey: Clave primaria por user_id
- user_username_key: Único por username
- idx_user_email: Índice B-tree por email
- idx_user_external_id: Índice B-tree por external_id
- idx_user_full_name_trgm: Índice GIN por full_name usando gin_trgm_ops
- idx_user_username: Índice B-tree por username
- idx_user_username_trgm: Índice GIN por username usando gin_trgm_ops
**Triggers:** Por confirmar
**Particionado:** Ninguna
**Observaciones:** El campo "full_name" es opcional y no tiene un valor por defecto. Los campos "last_login_at", "created_at" y "updated_at" tienen valores por defecto que actualizan automáticamente.
