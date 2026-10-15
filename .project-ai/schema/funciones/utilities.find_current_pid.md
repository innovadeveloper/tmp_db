## utilities.find_current_pid
**Proposito:** Devuelve el ID de proceso del backend de PostgreSQL que está ejecutando la función.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| Ninguno |

**Retorna:** Un entero que representa el ID de proceso del backend de PostgreSQL.

**Tablas que lee:** No lee ninguna tabla.

**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla.

**Funciones que invoca:** No invoca ninguna función.

**Logica paso a paso:**
1. La función invoca la función `pg_backend_pid()` de PostgreSQL, que devuelve el ID de proceso del backend que está ejecutando la función.

**Errores y excepciones:** No lanza errores ni excepciones específicas.

**Observaciones:** La función es simple y no implica riesgos de seguridad o rendimiento significativos. No es necesario declararla como `SECURITY DEFINER` ni usar SQL dinámico.
