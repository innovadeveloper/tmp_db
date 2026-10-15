## api.get_routes
**Proposito:** Obtiene una lista de rutas filtradas según los criterios proporcionados, incluyendo información detallada sobre los puntos de control y terminales asociados.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.get_routes_input | Objeto de entrada que contiene los criterios de filtro para las rutas |

**Retorna:** Un objeto `api.get_routes_result` que contiene los resultados de la consulta, incluyendo detalles de las rutas, puntos de control y terminales.

**Tablas que lee:** 
- `core_operations.route`
- `shared.company`
- `core_operations.checkpoint`
- `core_operations.route_control`
- `core_operations.route_polyline`

**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla.

**Funciones que invoca:** No invoca ninguna función externa.

**Logica paso a paso:**
1. Normaliza los filtros proporcionados en `p_input`.
2. Realiza validaciones para asegurar que los filtros sean válidos.
3. Ejecuta una consulta principal que filtra las rutas según los criterios.
4. Agrupa y resume los puntos de control y terminales por ruta.
5. Obtiene el nombre de los terminales de origen y destino.
6. Cuenta los puntos de control y las polylines por ruta.
7. Construye el resultado final con los detalles de las rutas y los resúmenes de puntos de control y terminales.

**Errores y excepciones:** 
- `INVALID_ROUTE_TYPE`: Si el tipo de ruta contiene valores inválidos.
- `COMPANY_NOT_FOUND`: Si uno o más `company_id` del filtro no existen.
- `INTERNAL_ERROR`: Para cualquier otro error inesperado.

**Observaciones:** 
- La función utiliza un enfoque de CTE (Common Table Expressions) para organizar la lógica y mejorar la legibilidad.
- La función maneja excepciones generales y devuelve un código de error y un mensaje descriptivo en caso de fallo.
- La función no modifica ninguna tabla, lo que la hace segura para ser ejecutada por cualquier usuario.
