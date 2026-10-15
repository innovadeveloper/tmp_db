## api.create_monthly_partitions
**Proposito:** Crea particiones mensuales para tablas especificadas en un esquema, avanzando un número determinado de meses en el futuro.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_months_ahead | integer | Número de meses en el futuro para crear particiones. Debe estar entre 0 y 12. |

**Retorna:** Un objeto `api.create_monthly_partitions_result` que contiene el resultado de la operación, incluyendo detalles de cada partición creada, existente o con error.

**Tablas que lee:** `pg_class`, `pg_namespace`.

**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla directamente, pero puede crear nuevas particiones.

**Funciones que invoca:** `TO_CHAR`, `FORMAT`, `EXECUTE`.

**Logica paso a paso:**
1. Valida que `p_months_ahead` esté entre 0 y 12.
2. Itera desde el mes actual hasta `p_months_ahead` meses en el futuro.
3. Para cada mes, itera sobre las tablas especificadas en `v_monthly_tables`.
4. Verifica si la partición ya existe.
5. Si no existe, construye y ejecuta el DDL para crear la partición.
6. Registra el resultado de cada operación (creada, existente, error).
7. Devuelve un objeto `api.create_monthly_partitions_result` con el resumen de la operación.

**Errores y excepciones:** 
- Si `p_months_ahead` no está entre 0 y 12, devuelve un error con código `INVALID_MONTHS_AHEAD`.
- Si ocurre un error al crear una partición, registra el error y continúa con las siguientes.

**Observaciones:** 
- La función es segura (`SECURITY DEFINER`).
- Utiliza SQL dinámico para crear las particiones.
- No modifica ninguna tabla existente, solo crea nuevas particiones.
