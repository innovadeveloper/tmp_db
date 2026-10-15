## listener.notify_permission_change
**Proposito:** Notifica a través de una señal de PostgreSQL cualquier cambio en las tablas que la invocan.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| Por confirmar | Por confirmar | Por confirmar |

**Retorna:** `NULL`
**Tablas que lee:** No lee ninguna tabla.
**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla.
**Funciones que invoca:** `pg_notify`, `json_build_object`, `extract`
**Logica paso a paso:**
1. Construye un objeto JSON con el nombre de la tabla, la operación realizada y el timestamp actual.
2. Envía una señal llamada 'permissions_changed' con el objeto JSON como payload.
3. Retorna `NULL`.
**Errores y excepciones:** No especifica errores o excepciones.
**Observaciones:** La función es un disparador que se ejecuta automáticamente en respuesta a ciertas operaciones en las tablas que la invocan. No tiene riesgos de seguridad adicionales, pero es importante que las tablas que la invocan estén correctamente configuradas para evitar notificaciones innecesarias o mal formadas.
