## api._generate_driver_code
**Proposito:** Genera un código de conductor único basado en un prefijo configurado y un número secuencial.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| Ninguno |

**Retorna:** Un código de conductor como `character varying`.

**Tablas que lee:** 
- `shared.configuration`: Para obtener el prefijo del código del conductor.
- `hr.driver`: Para buscar el siguiente número secuencial disponible.

**Tablas que modifica (INSERT/UPDATE/DELETE):** 
- No modifica ninguna tabla.

**Funciones que invoca:** 
- No invoca ninguna función.

**Logica paso a paso:** 
1. Obtiene el prefijo del código del conductor desde la tabla `shared.configuration`.
2. Filtra y busca el siguiente número secuencial disponible en la tabla `hr.driver`.
3. Genera el código de conductor concatenando el prefijo y el número secuencial.
4. Verifica si el código generado ya existe en la tabla `hr.driver`. Si existe, incrementa el número secuencial y vuelve a intentar.
5. Devuelve el código de conductor generado.

**Errores y excepciones:** 
- No se especifican excepciones específicas en el código.

**Observaciones:** 
- El prefijo del código del conductor se obtiene de la configuración y puede ser modificado.
- El código genera un número secuencial que debe ser único y sigue un formato específico.
- El código utiliza una bucle `WHILE` para asegurarse de que el código generado no exista en la tabla `hr.driver`.
