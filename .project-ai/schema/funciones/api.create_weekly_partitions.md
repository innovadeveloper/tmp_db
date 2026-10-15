## api.create_weekly_partitions
**Proposito:** Crea particiones semanales para tablas especificadas en un rango de semanas determinado.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_weeks_ahead | integer | Número de semanas a adelantar desde la fecha actual para crear particiones. Debe estar entre 0 y 52. |

**Retorna:** Un objeto `api.create_monthly_partitions_result` que contiene el resultado de la operación, incluyendo detalles de cada partición creada, existente o con errores.

**Tablas que lee:** `pg_class`, `pg_namespace`.

**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla directamente, pero puede crear nuevas particiones.

**Funciones que invoca:** `TO_CHAR`, `LPAD`, `FORMAT`, `EXECUTE`.

**Logica paso a paso:**
1. Valida que `p_weeks_ahead` esté entre 0 y 52.
2. Inicia un bucle para cada semana en el rango especificado.
3. Para cada semana, calcula el rango de fechas (inicio y fin de la semana).
4. Para cada tabla en la lista de tablas semanales, verifica si la partición ya existe.
5. Si la partición no existe, la crea utilizando una DDL dinámica.
6. Registra el resultado de la operación para cada partición (creada, existente o con errores).
7. Devuelve un objeto `api.create_monthly_partitions_result` con los detalles de la operación.

**Errores y excepciones:** 
- Si `p_weeks_ahead` no está entre 0 y 52, se lanza un error `INVALID_WEEKS_AHEAD`.
- Si ocurre cualquier otro error durante la ejecución, se lanza un error `INTERNAL_ERROR`.

**Observaciones:** 
- La función utiliza `SECURITY DEFINER` para ejecutar DDL dinámica.
- La lista de tablas semanales está codificada en la función y no puede ser modificada dinámicamente.
- La función no modifica ninguna tabla existente, solo crea nuevas particiones.
