## api.assign_roles_to_user
**Proposito:** Asigna o revoca roles a un usuario, validando los roles y los permisos del usuario.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.assign_roles_to_user_input | Objeto de entrada que contiene el usuario_id, roles a asignar y el usuario que realiza la asignación. |

**Retorna:** api.assign_roles_to_user_result - Objeto que contiene el resultado de la operación, incluyendo detalles de cada rol procesado.

**Tablas que lee:** identity."user", identity.role, identity.user_tenant_access, identity.user_role.

**Tablas que modifica (INSERT/UPDATE/DELETE):** identity.user_role.

**Funciones que invoca:** No invoca ninguna función externa.

**Logica paso a paso:**
1. Valida que el user_id no sea NULL.
2. Valida que el usuario exista y esté activo.
3. Valida que el assigned_by exista si se proporciona.
4. Valida que el array de roles no sea NULL.
5. Procesa cada rol en el array:
   - Valida que el role_id no sea NULL y no esté duplicado.
   - Valida que el rol exista y esté activo.
   - Valida que el usuario tenga acceso al tenant del rol.
   - Valida que expires_at no sea en el pasado.
   - Si el rol ya está activo para el usuario, lo marca como SKIPPED.
   - Si el rol no está activo, lo inserta en la tabla user_role.
6. Revoca roles activos que no están presentes en el payload.
7. Devuelve un objeto con el resultado global y detalles de cada rol procesado.

**Errores y excepciones:** 
- Si ocurre un error inesperado, se captura y se devuelve un error interno con el mensaje de error.

**Observaciones:** 
- La función es segura para definir (SECURITY DEFINER).
- No utiliza SQL dinámico.
- La función maneja errores y excepciones para asegurar una respuesta consistente.
