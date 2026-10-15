## utilities.create_gps_partition
**Proposito:** Crea una nueva partición de la tabla `gps_raw_event` en la base de datos `fleet` para un mes específico.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_timestamp | timestamp with time zone | Fecha y hora para la cual se creará la partición |

**Retorna:** void
**Tablas que lee:** pg_class, pg_namespace
**Tablas que modifica (INSERT/UPDATE/DELETE):** fleet.gps_raw_event
**Funciones que invoca:** format, date_trunc, to_char
**Logica paso a paso:**
1. Determina el inicio del mes a partir de la fecha proporcionada.
2. Determina el inicio del siguiente mes.
3. Construye el nombre de la partición basado en el año y mes.
4. Verifica si la partición ya existe en el esquema `fleet`.
5. Si la partición no existe, la crea utilizando la sentencia `CREATE TABLE ... PARTITION OF`.

**Errores y excepciones:** No se especifican excepciones específicas en el código.

**Observaciones:** La función utiliza SQL dinámico para crear la partición, lo que permite una flexibilidad en la creación de particiones según la fecha proporcionada. La seguridad de la función se basa en la autorización del usuario que la ejecuta, ya que no se utiliza `SECURITY DEFINER`.
