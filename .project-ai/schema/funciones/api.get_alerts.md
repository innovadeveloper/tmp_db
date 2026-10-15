## api.get_alerts
**Proposito:** Consulta paginada de alertas con filtros opcionales. Paginado por keyset (cursor) sobre (alert_timestamp DESC, alert_id DESC). Siempre aplica rango de fechas para activar partition pruning — default últimas 24h. page_size: 1-200, default 50. Pasar next_cursor del resultado anterior para avanzar.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.get_alerts_input | Objeto de entrada con filtros y paginación |

**Retorna:** api.get_alerts_result
**Tablas que lee:** core_operations.alert, core_operations.alert_type
**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla
**Funciones que invoca:** No invoca ninguna función
**Logica paso a paso:** 
1. Valida los parámetros de entrada (status, severity, page_size, date_from, date_to).
2. Construye la consulta principal con los filtros aplicados y ordena por alert_timestamp DESC, alert_id DESC.
3. Utiliza un CTE (Common Table Expression) para aplicar el límite de página y mantener la partición de datos.
4. Genera el resultado paginado, detecta si hay siguiente página y normaliza los datos.
5. Maneja excepciones y retorna un resultado con éxito o error.
**Errores y excepciones:** 
- INVALID_STATUS: El status proporcionado no es válido.
- INVALID_SEVERITY: La severidad proporcionada no es válida.
- INVALID_PAGE_SIZE: El page_size está fuera del rango permitido (1-200).
- INVALID_DATE_RANGE: date_from es posterior a date_to.
- INTERNAL_ERROR: Error interno inesperado.
**Observaciones:** 
- La función utiliza un patrón de paginación por keyset para mejorar el rendimiento.
- Aplica rango de fechas para activar la partición de datos.
- El page_size tiene un rango limitado (1-200) y un valor por defecto de 50.
- La función maneja excepciones y retorna un resultado consistente.
