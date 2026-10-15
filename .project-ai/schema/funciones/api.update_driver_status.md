## api.update_driver_status
**Proposito:** Actualiza el estado de un conductor en el sistema, incluyendo su disponibilidad y fecha de terminación, y registra el cambio en el log de actividades.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.update_driver_status_input | Objeto de entrada que contiene los detalles del conductor a actualizar y la nueva información de estado. |

**Retorna:** api.update_driver_status_result - Un objeto que indica el éxito o fracaso de la operación, junto con detalles del conductor actualizados y el ID del registro de actividad.

**Tablas que lee:** 
- hr.driver
- hr.person
- shared.configuration

**Tablas que modifica (INSERT/UPDATE/DELETE):** 
- hr.driver
- identity.activity_log

**Funciones que invoca:** 
- No se invocan funciones externas.

**Logica paso a paso:** 
1. Valida que el nuevo estado de empleo sea uno de los permitidos (ACTIVE, SUSPENDED, TERMINATED).
2. Verifica si el conductor existe en la base de datos.
3. Asegura que el cambio no sea un no-op (el conductor ya tiene el nuevo estado).
4. Si el estado es TERMINATED a ACTIVE, verifica si la reactivación está permitida según la configuración.
5. Construye los cambios antes y después para el registro de actividad.
6. Actualiza el estado del conductor en la tabla hr.driver.
7. Registra el cambio en la tabla identity.activity_log.
8. Devuelve los detalles del conductor actualizados y el ID del registro de actividad.

**Errores y excepciones:** 
- INVALID_EMPLOYMENT_STATUS: El nuevo estado de empleo no es válido.
- DRIVER_NOT_FOUND: El conductor especificado no existe.
- INVALID_STATUS_TRANSITION: La transición de estado no es permitida.
- INTERNAL_ERROR: Error interno inesperado.

**Observaciones:** 
- La función es segura para definir (SECURITY DEFINER).
- No se utiliza SQL dinámico.
- La función maneja excepciones generales y devuelve un mensaje de error descriptivo.
