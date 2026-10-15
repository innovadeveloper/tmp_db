## api.invalidate_user_session
**Proposito:** Invalida una sesión de usuario, ya sea por `session_id`, `token` o `user_id`. Si se proporciona `user_id`, invalida todas las sesiones activas del usuario. Si se proporciona `session_id` o `token`, invalida solo esa sesión específica.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.invalidate_user_session_input | Objeto de entrada que contiene `session_id`, `token`, y `user_id`. Al menos uno de estos debe proporcionarse. |

**Retorna:** `api.invalidate_user_session_result`, que contiene el resultado de la operación, detalles de las sesiones invalidadas, y posibles errores.

**Tablas que lee:** `identity.user_session`

**Tablas que modifica (INSERT/UPDATE/DELETE):** `identity.user_session`

**Funciones que invoca:** `None`

**Logica paso a paso:**
1. Valida que se proporcione al menos `session_id`, `token`, o `user_id`.
2. Si se proporciona `user_id`, valida que el usuario exista.
3. Si se proporciona `user_id`, captura los detalles de las sesiones activas del usuario.
4. Invalida todas las sesiones activas del usuario.
5. Si se proporciona `session_id` o `token`, busca la sesión específica.
6. Si la sesión está inactiva, genera un aviso.
7. Invalida la sesión específica.
8. Retorna los detalles de las sesiones invalidadas y el resultado de la operación.

**Errores y excepciones:**
- `MISSING_IDENTIFIER`: No se proporcionó `session_id`, `token`, ni `user_id`.
- `USER_NOT_FOUND`: El `user_id` proporcionado no existe.
- `SESSION_NOT_FOUND`: La sesión con el `session_id` o `token` proporcionado no existe.
- `SESSION_ALREADY_INACTIVE`: La sesión ya estaba inactiva.
- `INTERNAL_ERROR`: Error interno inesperado.

**Observaciones:** La función utiliza `SECURITY DEFINER` para ejecutar operaciones en nombre del usuario que la invoca. No utiliza SQL dinámico.
