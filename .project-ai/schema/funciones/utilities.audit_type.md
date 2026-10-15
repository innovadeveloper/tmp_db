## utilities.audit_type
**Proposito:** Genera un informe detallado sobre la estructura y las funciones que utilizan un tipo de datos específico en PostgreSQL.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_type_name | text | Nombre del tipo de datos para el que se genera el informe |

**Retorna:** Una tabla con dos columnas: `section` y `detail`. La columna `section` indica si la información pertenece a la estructura del tipo o a las funciones que lo usan. La columna `detail` contiene los detalles específicos.

**Tablas que lee:** `pg_attribute`, `pg_type`, `pg_depend`, `pg_proc`, `pg_namespace`

**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla.

**Funciones que invoca:** No invoca ninguna función externa.

**Logica paso a paso:**
1. Recupera la estructura del tipo especificado (`p_type_name`) utilizando la información de las tablas `pg_attribute` y `pg_type`.
2. Recupera las funciones que utilizan el tipo especificado utilizando la información de las tablas `pg_type`, `pg_depend`, `pg_proc` y `pg_namespace`.

**Errores y excepciones:** No se manejan errores específicos en el código proporcionado.

**Observaciones:** La función es segura para definir (`SECURITY DEFINER`) y no utiliza SQL dinámico.
