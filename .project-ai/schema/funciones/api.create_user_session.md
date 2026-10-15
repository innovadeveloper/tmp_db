## api.create_user_session
**Proposito:** Crea una nueva sesión de usuario y devuelve información sobre la sesión creada y las sesiones concurrentes del usuario.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.create_user_session_input | Objeto de entrada que contiene los detalles de la sesión a crear, como user_id, token, ip_address, user_agent y expires_at. |

**Retorna:** api.create_user_session_result - Un objeto que contiene el resultado de la operación, incluyendo el éxito de la operación, mensajes de error, detalles de la sesión creada y información sobre las sesiones concurrentes del usuario.

**Tablas que lee:** identity.user, identity.user_session, shared.configuration

**Tablas que modifica (INSERT/UPDATE/DELETE):** identity.user_session

**Funciones que invoca:** Por confirmar

**Logica paso a paso:**
1. Valida si el usuario existe y está activo.
2. Valida si el token ya existe en el sistema.
3. Valida si la fecha de expiración es futura.
4. Lee el límite de sesiones concurrentes desde la configuración.
5. Cuenta las sesiones activas vigentes del usuario.
6. Recopila los detalles de las sesiones concurrentes.
7. Valida si el límite de sesiones concurrentes ha sido alcanzado.
8. Inserta la nueva sesión en la tabla identity.user_session.
9. Pobla el resultado con los detalles de la sesión creada y las sesiones concurrentes.

**Errores y excepciones:**
- unique_violation: Se lanza si ocurre una violación de la restricción única en la tabla identity.user_session.
- Otros errores: Se lanza un error interno con el mensaje de error correspondiente.

**Observaciones:** La función es segura y se ejecuta con el privilegio SECURITY DEFINER, lo que permite que cualquier usuario invoque la función sin restricciones adicionales.
