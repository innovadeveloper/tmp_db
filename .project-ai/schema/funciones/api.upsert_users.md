## api.upsert_users
**Proposito:** La función `api.upsert_users` es un procedimiento que permite insertar o actualizar usuarios en la base de datos, gestionando tanto los datos del usuario como sus accesos a diferentes inquilinos (tenants). La función valida los datos de entrada, verifica la existencia de usuarios y accesos duplicados, y realiza las operaciones correspondientes (INSERT o UPDATE) en las tablas `identity."user"` y `identity.user_tenant_access`.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.upsert_users_input | Un objeto que contiene un array de usuarios a ser insertados o actualizados. |

**Retorna:** Un objeto `api.upsert_users_result` que contiene el resultado de la operación, incluyendo el estado de éxito, el número de usuarios procesados, insertados, actualizados y omitidos, así como detalles de cualquier error ocurrido.

**Tablas que lee:** 
- `identity.tenant`
- `identity."user"`
- `identity.user_tenant_access`

**Tablas que modifica (INSERT/UPDATE/DELETE):** 
- `identity."user"`
- `identity.user_tenant_access`

**Funciones que invoca:** 
- `NULL`

**Logica paso a paso:** 
1. Valida que el array de usuarios no sea `NULL` ni vacío.
2. Recorre cada usuario en el array de entrada.
3. Realiza validaciones generales como la existencia del `tenant_id` y la unicidad del `external_id`.
4. Busca el usuario en la base de datos por `external_id`.
5. Si el usuario existe, verifica si hay cambios en los campos `username`, `email`, `full_name` o `is_active`. Si hay cambios, actualiza el usuario; si no, marca como omitido.
6. Si el usuario no existe, verifica la unicidad del `username` y `email`, y luego inserta el nuevo usuario.
7. Para cada usuario, intenta actualizar o insertar su acceso a los inquilinos (tenants) en la tabla `identity.user_tenant_access`.
8. Registra el resultado de cada operación (INSERT, UPDATE, SKIP, ERROR) en el objeto de resultado.
9. Devuelve el objeto de resultado con los detalles de la operación.

**Errores y excepciones:** 
- `NULL_USERS_ARRAY`: El array de usuarios es `NULL`.
- `NO_USERS_PROVIDED`: El array de usuarios está vacío.
- `MISSING_EXTERNAL_ID`: El campo `external_id` es obligatorio y no puede estar vacío.
- `MISSING_TENANT_ID`: El campo `tenant_id` es obligatorio.
- `TENANT_NOT_FOUND`: El `tenant_id` no existe o está inactivo.
- `GRANTED_BY_NOT_FOUND`: El `granted_by` no existe o está inactivo.
- `DUPLICATE_EXTERNAL_ID_IN_BATCH`: El `external_id` aparece más de una vez en el mismo lote.
- `DUPLICATE_USERNAME`: El `username` ya está asignado a otro usuario en la base de datos.
- `DUPLICATE_USERNAME_IN_BATCH`: El `username` ya fue asignado en este lote.
- `DUPLICATE_EMAIL`: El `email` ya está registrado para otro usuario en la base de datos.
- `DUPLICATE_EMAIL_IN_BATCH`: El `email` ya fue asignado en este lote.
- `MISSING_USERNAME`: El campo `username` es obligatorio al crear un usuario.
- `MISSING_EMAIL`: El campo `email` es obligatorio al crear un usuario.
- `INTERNAL_ERROR`: Error interno inesperado.

**Observaciones:** 
- La función utiliza transacciones implícitas para asegurar que las operaciones de inserción y actualización sean atómicas.
- La validación de duplicados se realiza tanto en el lote como en la base de datos.
- Los errores en la operación de `user_tenant_access` no revierten la operación del usuario, sino que se registran en `tenant_access_status`.
- La función no utiliza funciones adicionales y no es definida como `SECURITY DEFINER`, por lo que no tiene privilegios adicionales sobre las tablas.
