## api.deduct_license_points
**Proposito:** Esta función se utiliza para deducir puntos de licencia a un conductor y registrar el cambio en el sistema.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.deduct_license_points_input | Un objeto que contiene los datos de entrada necesarios para la operación, como el ID del conductor, la cantidad de puntos a deducir, el motivo de la deducción y el ID del usuario que realiza el cambio. |

**Retorna:** Un objeto `api.deduct_license_points_result` que contiene el resultado de la operación, incluyendo el éxito o fracaso, mensajes de error, y detalles sobre el cambio realizado.

**Tablas que lee:** 
- `hr.driver`: Para obtener los detalles del conductor.
- `hr.person`: Para obtener los detalles de la persona asociada al conductor.
- `shared.configuration`: Para obtener el umbral mínimo de puntos de licencia.

**Tablas que modifica (INSERT/UPDATE/DELETE):** 
- `hr.driver`: Para actualizar los puntos de licencia y el estado de disponibilidad del conductor.
- `identity.activity_log`: Para registrar el cambio en el historial de actividades.

**Funciones que invoca:** No se invocan otras funciones dentro de esta función.

**Logica paso a paso:**
1. **Validación 1:** Verifica que la cantidad de puntos a deducir sea mayor que 0.
2. **Validación 2:** Verifica que el conductor exista en la base de datos.
3. **Validación 3:** Verifica si el conductor ya tiene 0 puntos de licencia.
4. **Cálculo de puntos:** Calcula los puntos de licencia restantes después de la deducción, asegurando que no sean negativos.
5. **Leer umbral mínimo:** Obtiene el umbral mínimo de puntos de licencia desde la configuración.
6. **Determinar bloqueo de despacho:** Determina si el despacho del conductor debe ser bloqueado basado en los puntos restantes y el estado de empleo del conductor.
7. **Construir cambios:** Construye un JSON que registra los cambios antes y después de la operación.
8. **Actualizar conductor:** Actualiza los puntos de licencia y el estado de disponibilidad del conductor en la tabla `hr.driver`.
9. **Registrar actividad:** Registra el cambio en el historial de actividades en la tabla `identity.activity_log`.
10. **Devolver resultado:** Devuelve un objeto `api.deduct_license_points_result` con los detalles del resultado de la operación.

**Errores y excepciones:** 
- `INVALID_POINTS_AMOUNT`: La cantidad de puntos a deducir debe ser mayor a 0.
- `DRIVER_NOT_FOUND`: El conductor no existe.
- `POINTS_ALREADY_ZERO`: El conductor ya tiene 0 puntos de licencia.
- `INTERNAL_ERROR`: Error interno inesperado.

**Observaciones:** 
- La función utiliza `SECURITY DEFINER` para ejecutarse con los privilegios del usuario que la define.
- La función puede ejecutar SQL dinámico al leer el umbral mínimo de puntos de licencia desde la configuración.
