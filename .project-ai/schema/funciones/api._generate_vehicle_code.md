## api._generate_vehicle_code
**Proposito:** Genera un código de vehículo único basado en un prefijo configurado y un contador secuencial.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| Ninguno |

**Retorna:** Un código de vehículo como una cadena de caracteres (`character varying`).

**Tablas que lee:** 
- `shared.configuration`: Para obtener el prefijo de código de vehículo.
- `fleet.vehicle`: Para obtener el siguiente número secuencial disponible.

**Tablas que modifica (INSERT/UPDATE/DELETE):** 
- No modifica ninguna tabla.

**Funciones que invoca:** 
- No invoca ninguna función.

**Logica paso a paso:**
1. Obtiene el prefijo de código de vehículo desde la tabla `shared.configuration`.
2. Si el prefijo es nulo o vacío, lo establece como 'BUS'.
3. Busca el siguiente número secuencial disponible en la tabla `fleet.vehicle` que tenga un código de vehículo que comience con el prefijo y un número secuencial.
4. Incrementa el número secuencial y lo formatea con ceros a la izquierda para que tenga un formato de 3 dígitos.
5. Genera el código de vehículo concatenando el prefijo y el número secuencial.
6. Verifica si el código generado ya existe en la tabla `fleet.vehicle`. Si existe, incrementa el número secuencial y vuelve a intentar hasta que encuentre un código único.
7. Devuelve el código de vehículo generado.

**Errores y excepciones:** 
- No se manejan excepciones específicas en el código proporcionado.

**Observaciones:** 
- La función utiliza un bucle `WHILE` para protegerse contra colisiones concurrentes, lo que puede afectar el rendimiento si hay muchos intentos de generación simultáneos.
- La función asume que los códigos de vehículo existentes siguen un formato específico (prefijo seguido de un número).
