## api.assign_role_to_user
**Proposito:** Asigna un rol a un usuario, validando su existencia, actividad, acceso al tenant y si la asignación ya no existe.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.assign_role_to_user_input | Objeto de entrada que contiene los detalles de la asignación de rol, incluyendo user_id, role_id, assigned_by, expires_at, etc. |

**Retorna:** api.assign_role_to_user_result, que contiene el resultado de la operación, incluyendo success, error_code, error_message, user_role_id, user_id, role_id, tenant_id, is_active, assigned_by, assigned_at, expires_at, role_name y is_temporary.

**Tablas que lee:** identity.user, identity.role, identity.user_tenant_access, identity.user_role.

**Tablas que modifica (INSERT/UPDATE/DELETE):** identity.user_role.

**Funciones que invoca:** Por confirmar.

**Logica paso a paso:**
1. Valida si el usuario existe.
2. Valida si el rol existe y está activo.
3. Valida si el usuario tiene acceso al tenant del rol.
4. Valida si la asignación activa ya existe.
5. Valida si expires_at no es en el pasado.
6. Inserta la asignación del rol al usuario.
7. Pobla el resultado con los detalles de la asignación.

**Errores y excepciones:**
- unique_violation: Conflicto de unicidad, indica que el rol ya fue asignado concurrentemente.
- Otros errores: Devuelve un error interno con el mensaje de error correspondiente.

**Observaciones:** La función utiliza un bloque TRY-CATCH para manejar excepciones, incluyendo errores de unicidad y errores internos. La función es definida con SECURITY DEFINER, lo que significa que se ejecutará con los privilegios del usuario que la definió, no del usuario que la invoca.
