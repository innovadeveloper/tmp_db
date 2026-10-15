## api.get_user_session
**Proposito:** Obtiene la sesión de un usuario para un tenant específico, validando los identificadores de usuario y el acceso al tenant.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.get_user_session_input | Objeto de entrada que contiene el tenant_id y el identificador de usuario (user_id o external_id). |

**Retorna:** Un objeto `api.get_user_session_result` que contiene la información del usuario y el acceso al tenant, o un error si la validación falla.

**Tablas que lee:** `identity."user"`, `identity.user_tenant_access`

**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla.

**Funciones que invoca:** No invoca ninguna función externa.

**Logica paso a paso:**
1. Valida que `tenant_id` no sea nulo.
2. Valida que se proporcione exactamente un identificador de usuario (`user_id` o `external_id`).
3. Realiza una consulta única que une la tabla de usuarios con la tabla de acceso al tenant.
4. Si no se encuentra el usuario o el acceso al tenant, devuelve un error correspondiente.
5. Si la consulta es exitosa, retorna la información del usuario y el acceso al tenant.

**Errores y excepciones:**
- `MISSING_TENANT_ID`: El `tenant_id` es obligatorio.
- `MISSING_USER_IDENTIFIER`: Debe proporcionar `user_id` o `external_id`.
- `AMBIGUOUS_USER_IDENTIFIER`: No puede proporcionar ambos `user_id` y `external_id`.
- `USER_NOT_FOUND`: El usuario no existe.
- `TENANT_ACCESS_NOT_FOUND`: El usuario no tiene acceso al tenant.
- `INTERNAL_ERROR`: Error interno inesperado.

**Observaciones:** La función es `STABLE`, lo que permite que el plan de ejecución sea cacheado. La consulta utiliza índices `btree` en las columnas de búsqueda para mejorar el rendimiento.
