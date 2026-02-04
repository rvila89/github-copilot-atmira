# 🤖 PR Documenter — Agente de Análisis Funcional y Documentación de Pull Requests (Formato Banca March)
Agente personalizado de GitHub Copilot que analiza los cambios entre la rama actual y la rama destino en un repositorio Git, identifica su impacto funcional y genera documentación en Markdown siguiendo estrictamente el Formato Banca March. Se enfoca en flujos, reglas de negocio y comportamientos modificados, no en archivos individuales.
Índice

**Autor(es):** Francisco José Mellado  
**Equipo/Área responsable:** Banca March Front
**Fecha de creación:** [2026-01-08]  
**Última actualización:** [2026-02-03]  
**Equipos o proyectos que lo utilizan:**  
- [NO-BOL/BANCA MARCH FRONT]  

## Índice
- [Descripción](#descripción)
- [Características clave](#características-clave)
- [Herramientas que utiliza](#herramientas-que-utiliza)
- [Requisitos previos](#requisitos-previos)
- [Instalación / Configuración en GitHub Copilot](#instalación--configuración-en-github-copilot)
- [Uso](#uso)
- [Formato de salida obligatorio (Formato Banca March)](#formato-de-salida-obligatorio-formato-banca-march)
- [Ejemplos de prompts](#ejemplos-de-prompts)
- [Consejos de uso](#consejos-de-uso)
- [Resolución de problemas](#resolución-de-problemas)
- [Seguridad y privacidad](#seguridad-y-privacidad)
- [Estructura recomendada de carpeta en proyecto](#estructura-recomendada-de-carpeta-en-proyecto)


## Descripción
PR Documenter actúa como un Asistente Experto en Análisis Funcional y Documentación Técnica. A partir de un repositorio Git abierto en tu IDE, el agente:

Detecta la rama actual y deriva la clave JIRA, rama base y rama destino siguiendo la convención -TO-<DESTINO>.
Compara la rama actual con la rama destino (sin modificar nada) para extraer el diff real del Pull Request.
Analiza la lógica introducida o modificada (validaciones, flujos, reglas, integraciones) agrupando por cambios funcionales (no por archivos).
Genera un documento Markdown con 4 secciones exactas (Resumen, Cambios clave, Cómo probar, Evidencia visual) en el Formato Banca March.

Este agente no ejecuta comandos que alteren el repositorio ni el histórico. Solo lee y documenta.

## Características clave

- 🔎 **Análisis funcional de cambios:** impacto en reglas de negocio, flujos, validaciones e integraciones.
- 🧭 **Agrupación por lógica, no por archivo:** enfocado en el comportamiento de la aplicación.
- 🧾 **Salida estandarizada:** Formato Banca March con 4 secciones obligatorias.
- 🧼 **Exclusión automática:** tests/specs/mocks fuera del análisis funcional.
- 🧠 **Buenas prácticas:** Clean Code, SOLID, convenciones por lenguaje.
- 🛡️ **Modo lectura:** sin acciones que modifiquen el repo (commit, push, merge, etc.).

## Herramientas que utiliza

- `codebase`: inspección de archivos del repo cuando el IDE lo permite.
- `changes`: acceso al diff/contexto de cambios cuando la integración lo expone.
- `runCommands/getTerminalOutput`: comandos de lectura (`git rev-parse`, `git diff`, `git diff --name-only`, `git log`, etc.).
- `runCommands/runInTerminal`: solo lectura para obtener salidas de Git.

> Nunca ejecuta comandos destructivos: `git commit`, `git push`, `git merge`, `git rebase`, `git checkout`, `git reset`, `git rm`, etc.

## Requisitos previos

- IDE con GitHub Copilot Chat y soporte para Agentes Personalizados.
- Repositorio Git abierto y con acceso a las ramas relevantes.
- Convención de ramas que incluya `-TO-<DESTINO>` (p. ej., `PROJ-1234-nueva-funcionalidad-TO-TEST`).

## Instalación / Configuración en GitHub Copilot

1. Abre Copilot Chat en tu IDE.
2. Ve a Agentes (Custom/Personalizados).
3. Crea un nuevo agente y nómbralo: **PR Documenter**.
4. Pega el contenido del archivo `pr-documenter.agent.md` (incluido junto a este README).
5. Guarda y verifica que el agente aparece en la lista de disponibles.

## Uso

### Flujo rápido

1. Selecciona el agente: abre Copilot Chat y elige **PR Documenter**.
2. Sitúate en el proyecto: asegúrate de que el workspace del repo está abierto.
3. Lanza la documentación: pide al agente que genere la documentación de los cambios de tu rama actual contra la rama destino.
4. Revisa el Markdown generado (4 secciones) y ajusta la parte de **Cómo probar** y **Evidencia visual** si aplica.
5. Copia el bloque final y pégalo en la descripción del Pull Request.

### Qué hace internamente

Detecta rama actual:

```sh
git rev-parse --abbrev-ref HEAD
```
Extrae:
- Clave JIRA: patrón `[A-Z]+-[0-9]+`
- Rama destino: desde sufijo `-TO-<DESTINO>` (p. ej., `DEV`, `TEST`, `MASTER`, `RELEASE/...`)
- Rama base: nombre de la rama sin el sufijo `-TO-<DESTINO>`

Obtiene el diff real del PR:

```sh
git diff <rama-destino>...<rama-actual>
```

Lista de archivos modificados (excluye test/spec/mock):

```sh
git diff --name-only <rama-destino>...<rama-actual>
```

> El análisis se centra en lógica funcional (no en archivos) y limita cada cambio a **máximo 2 líneas**.

## Formato de salida obligatorio (Formato Banca March)

El agente siempre devuelve un documento Markdown con estas **4 secciones exactas**. Estructura esperada:

```markdown
### Rama base: <rama-sin-sufijo-TO-destino>
### JIRA asociado: https://jira.bancamarch.es/browse/<clave-jira>

1. **Resumen**
	- Visión de alto nivel:
	  - Objetivos funcionales cumplidos
	  - Áreas del código afectadas (componentes, servicios, módulos)
	  - Tipo de cambio (nueva funcionalidad, refactorización, corrección, integración)
	- Debe ser un listado de cambios aunque solo haya uno
	- El resumen SIEMPRE debe tener menos puntos que “Cambios clave”

2. **Cambios clave**
	- ANÁLISIS DE LA LÓGICA MODIFICADA (NO agrupar por ficheros)
	- Cada punto debe explicar QUÉ cambió en la lógica de funcionamiento
	- Máximo 2 líneas por cambio
	- Enfoque en flujos, comportamientos, reglas de negocio modificadas
	- Ejemplo correcto: “Se añade validación de edad mínima antes de procesar la solicitud, rechazando automáticamente usuarios menores de 18 años”
	- Ejemplo incorrecto: “Cambios en el componente usuario.component.ts”

3. **Cómo probar**
	- Pasos para verificar la funcionalidad — requiere aportación del desarrollador

4. **Evidencia visual**
	- Capturas o videos demostrativos — requiere aportación del desarrollador
```

## Ejemplos de prompts

- **Documentar PR actual (camino feliz):**
	- “Genera la documentación de los cambios de mi rama actual siguiendo el Formato Banca March. Entrega las 4 secciones exactas. Excluye tests/specs/mocks y agrupa por cambios funcionales.”

## Consejos de uso

- Cumple la convención de ramas con sufijo `-TO-<DESTINO>` para extraer destino automáticamente.
- Incluye contexto en el prompt si el proyecto es complejo (módulo, servicio, feature).
- Si el diff es muy extenso, pide “trabajar por módulos/áreas lógicas”.
- En “Cómo probar”, añade los pasos de QA específicos (datos, endpoints, roles, precondiciones).
- Si hay cambios transversales (p. ej., validaciones comunes), pide al agente etiquetar claramente cada cambio con el flujo afectado.

## Resolución de problemas

- **No aparecen 4 secciones exactas**
	- Repite: “usa el Formato de salida obligatorio (Formato Banca March)”.

- **Lenguaje o framework no detectado**
	- Indícalo en el prompt o aporta rutas de archivos relevantes.

- **Branch destino no deducible**
	- Especifica: “compara contra develop/test/master/release/…”.

- **Aparecen tests/specs/mocks**
	- Indica: “excluye tests/specs/mocks del análisis funcional”.

- **Cambio descrito por archivo**
	- Pide: “no agrupes por archivos, reagrupa por cambios funcionales (reglas/flujo)”.

- **Salida demasiado larga o difusa**
	- Pide máximo 2 líneas por cambio y clasifica por flujo/regla.

## Seguridad y privacidad

- Solo lectura: el agente nunca ejecuta comandos que modifiquen el repo (commit, push, merge, rebase, checkout, reset, rm).
- No compartas secretos ni credenciales en los prompts o ejemplos.
- Valida la documentación con revisión técnica y, si aplica, con QA y stakeholders del dominio.
- Para cambios sensibles (p. ej., datos personales, riesgos de seguridad), añade notas de cumplimiento y controles en “Cómo probar”.

## Estructura recomendada de carpeta en proyecto
```text
.github/
└─ agents/
	└─ pr-documenter.agent.md   # Instrucciones del agente
```