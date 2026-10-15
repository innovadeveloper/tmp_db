## api.get_vehicles_last_position
**Proposito:** Obtiene la última posición de los vehículos de las empresas especificadas, incluyendo detalles del dispositivo GPS, la frescura de la señal y el conductor asignado.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.get_vehicles_last_position_input | Objeto de entrada que contiene los IDs de las empresas y otros parámetros de filtro. |

**Retorna:** Un objeto `api.get_vehicles_last_position_result` que contiene la lista de vehículos con sus últimas posiciones, detalles del dispositivo GPS, frescura de la señal y el conductor asignado. También incluye contadores de vehículos totales, con posición, con señal perdida y sin datos GPS.

**Tablas que lee:** 
- `fleet.vehicle`
- `fleet.gps_device`
- `fleet.gps_raw_event`
- `fleet.vehicle_assignment`
- `hr.driver`
- `hr.person`
- `shared.configuration`

**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla.

**Funciones que invoca:** No invoca ninguna función externa.

**Logica paso a paso:**
1. Valida que `company_ids` no sea nulo ni vacío.
2. Lee el umbral de señal perdida desde la configuración.
3. Calcula las ventanas de partición (semana actual y anterior).
4. Obtiene los vehículos activos dentro de las empresas especificadas.
5. Obtiene los dispositivos GPS activos vinculados a esos vehículos.
6. Busca el último evento GPS por vehículo en las últimas dos semanas.
7. Asigna el conductor activo para cada vehículo.
8. Ensambla el resultado final con la información de los vehículos, dispositivos GPS, posiciones, frescura de señal y conductores.
9. Calcula contadores de vehículos totales, con posición, con señal perdida y sin datos GPS.
10. Devuelve el resultado.

**Errores y excepciones:** 
- Si `company_ids` es nulo o vacío, devuelve un error con código `MISSING_COMPANY_IDS`.
- Si ocurre un error interno, devuelve un error con código `INTERNAL_ERROR` y el mensaje de error correspondiente.

**Observaciones:** 
- La función utiliza `DISTINCT ON` para obtener la última posición de cada vehículo de manera eficiente.
- La función puede ser ejecutada por cualquier usuario debido a la ausencia de `SECURITY DEFINER`.
- La función no realiza operaciones que puedan afectar el rendimiento significativamente.
