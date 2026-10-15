# AGENTS.md

> Generado: 2026-10-15T17:11:54+00:00 · `project-ai finalize`
> Lee este archivo antes de preguntar o editar código.

## 1. Proyecto

**Nombre**: `DBProjects`  
**Stack**: desconocido  
**Raíz**: `/Users/kenny/PropertyProjects/DBProjects`  

## 2. Comandos

_Sin comandos detectados — ejecuta `project-ai recon`._

## 3. Entorno

_Sin requisitos de entorno detectados._

## 4. Mapa

_Sin mapa disponible — ver `.project-ai/repo-map.md`._

## 5. Trampas conocidas

_(Sin entradas en el journal aún — se añaden tras triage.)_

## 6. Navegación

- `.project-ai/repo-map.md` — mapa compacto de símbolos (clases, firmas)
- `.project-ai/project.json` — datos completos del proyecto con evidencia
- `.project-ai/schema-map.md` — esquema SQL (tablas, vistas, funciones)

## Reglas de Trabajo (Prioridad Alta)

- **Transparencia**: Si tu respuesta se basa en una lectura parcial, dilo explícitamente.
- **Firma de métodos**: Antes de modificar un método, cita su firma actual tal como aparece en el archivo.
- **Sugerir ≠ Aplicar**: Cuando propongas cambios de código, pregunta explícitamente si debo pedirte que los apliques con edit/write, o si solo quieres mostrarlos.
- **Verificación previa**: Antes de proponer código nuevo, verifica si ya existe algo similar en el proyecto (grep de clases/dependencias relacionadas).
- Responde siempre en español.
- No afirmes formatos, valores, topics ni payloads sin haber leído el código que los genera. Cita archivo y línea.
- **Lectura completa obligatoria**: Antes de listar, resumir o modificar un archivo, léelo COMPLETO.
  Solo usa offset/limit si el archivo supera las 500 líneas, y en ese caso,
  sigue leyendo en bloques consecutivos hasta el final.
  NUNCA saltes a un offset arbitrario sin haber leído el rango anterior completo.
