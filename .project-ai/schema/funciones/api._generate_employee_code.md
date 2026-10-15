## api._generate_employee_code
**Proposito:** Genera un código de empleado único basado en un prefijo configurado y un número secuencial.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| Ninguno |

**Retorna:** Un código de empleado como una cadena de caracteres (`character varying`).

**Tablas que lee:** 
- `shared.configuration`: Para obtener el prefijo del código de empleado.
- `hr.personnel`: Para buscar el siguiente número secuencial disponible.

**Tablas que modifica (INSERT/UPDATE/DELETE):** 
- No modifica ninguna tabla.

**Funciones que invoca:** 
- No invoca ninguna función externa.

**Logica paso a paso:** 
1. Obtiene el prefijo del código de empleado desde la tabla `shared.configuration`.
2. Busca el siguiente número secuencial disponible en la tabla `hr.personnel` que siga el patrón `prefijo-NNNN`.
3. Genera el código de empleado concatenando el prefijo y el número secuencial.
4. Verifica si el código generado ya existe en la tabla `hr.personnel`. Si existe, incrementa el número secuencial y vuelve a intentar hasta encontrar un código único.
5. Devuelve el código de empleado generado.

**Errores y excepciones:** 
- No se manejan errores específicos en el código proporcionado.

**Observaciones:** 
- La función utiliza una protección contra colisiones concurrentes utilizando un bucle `WHILE` que incrementa el número secuencial hasta encontrar un código único.
- La función asume que el prefijo del código de empleado está configurado en la tabla `shared.configuration`. Si no está configurado, usa 'EMP' como prefijo por defecto.
- La función no modifica ninguna tabla, lo que la hace segura de ejecutarse en un entorno de producción.
