## utilities.reset_sequence
**Proposito:** Esta función reinicia la secuencia de una columna serial en una tabla específica.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_table | text | Nombre de la tabla que contiene la columna serial. |
| p_column | text | Nombre de la columna serial que se desea reiniciar. |

**Retorna:** void
**Tablas que lee:** p_table
**Tablas que modifica (INSERT/UPDATE/DELETE):** Por confirmar
**Funciones que invoca:** pg_get_serial_sequence
**Logica paso a paso:**
1. Obtiene el nombre de la secuencia asociada a la columna serial especificada en la tabla.
2. Ejecuta una consulta para establecer el valor de la secuencia en el valor máximo de la columna más uno, asegurando que la secuencia esté correctamente reiniciada.
**Errores y excepciones:** No se especifican excepciones en el código proporcionado.
**Observaciones:** La función utiliza SQL dinámico para ejecutar la consulta de establecimiento de la secuencia.
