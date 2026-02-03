# 🤖 Code Refactor — Agente de Refactorización y Modernización Multilenguaje

Agente personalizado de GitHub Copilot que refactoriza y moderniza código existente, generando una vista Antes / Después, aplicando buenas prácticas modernas e idiomáticas, y explicando claramente los cambios y sus beneficios. Mantiene la funcionalidad original salvo que se indique lo contrario o sea necesario para corregir errores evidentes.

**Autor(es):** ai-tools  
**Equipo/Área responsable:** atmira 
**Fecha de creación:** [AAAA-MM-DD]  
**Última actualización:** [AAAA-MM-DD]  
**Equipos o proyectos que lo utilizan:**  
- [Proyecto/Equipo 1]  

## Índice

- [Descripción](#descripción)
- [Características clave](#características-clave)
- [Lenguajes y contextos soportados](#lenguajes-y-contextos-soportados)
- [Requisitos previos](#requisitos-previos)
- [Instalación / Configuración en GitHub Copilot](#instalación--configuración-en-github-copilot)
- [Uso](#uso)
- [Formato de salida obligatorio](#formato-de-salida-obligatorio)
- [Ejemplos de prompts](#ejemplos-de-prompts)
- [Consejos de uso](#consejos-de-uso)
- [Resolución de problemas](#resolución-de-problemas)
- [Seguridad y privacidad](#seguridad-y-privacidad)
- [Estructura recomendada de carpeta en proyecto](#estructura-recomendada-de-carpeta-en-proyecto)

## Descripción

Code Refactor transforma código legado o desactualizado para mejorar legibilidad, estructura, rendimiento, testabilidad y compatibilidad con versiones modernas (p. ej., Java 21, .NET 8, Angular 17, Python 3.x). El agente:

- Analiza el fragmento aportado (selección del editor, archivo activo o código pegado).
- Moderniza usando APIs actuales y patrones recomendados (evitando deprecated).
- Reduce deuda técnica: duplica menos, simplifica anidaciones, separa responsabilidades.
- Devuelve una vista Antes (código original) → Después (refactorizado) → Explicación de los cambios con beneficios y consideraciones.

**Objetivo:** entregar un refactor claro, mantenible y listo para integrar, priorizando la equivalencia funcional salvo petición o corrección necesaria.

## Características clave

- 🧹 Refactorización estructural: extracción de métodos/clases, separación de responsabilidades, reducción de complejidad.
- ♻️ Modernización a la versión objetivo (idiomas/idiomas y frameworks) evitando APIs obsoletas.
- 📐 Buenas prácticas idiomáticas y estilo consistente con el ecosistema.
- 🧪 Preparación para tests: desacoplo, DI cuando aplique, puntos de extensión.
- 📝 Explicación clara de cambios, beneficios y riesgos/consideraciones.
- 🧰 Herramientas: codebase (contexto del repo), search (localización de patrones y referencias internas).

## Lenguajes y contextos soportados

- Java (incl. migración a Java 21, servicios, repositorios, REST)
- .NET (migración a .NET 8, controladores, Minimal APIs, servicios)
- Angular (actualización a Angular 17, componentes, servicios, RxJS)
- Python 3.x (scripts, módulos, FastAPI/Flask cuando aplique)
- TypeScript / JavaScript

> Cuando el proyecto usa un framework (Spring, ASP.NET, Angular…), el agente respeta sus convenciones y ciclos de vida.

## Requisitos previos

- IDE con GitHub Copilot Chat habilitado.
- Agente Code Refactor creado en Agentes Personalizados.
- Workspace del proyecto abierto para aprovechar el contexto (codebase).

Tres datos clave para mejores resultados:

1. Código original
2. Motivo principal (legibilidad, rendimiento, deuda técnica, modernización, tests…)
3. Lenguaje/versión objetivo (p. ej., “Java 21”)

## Instalación / Configuración en GitHub Copilot

1. Abre Copilot Chat en el IDE.
2. Ve a Agentes (Custom/Personalizados).
3. Crea un nuevo agente: Code Refactor.
4. Pega el contenido del archivo `code-refactor.agent.md`.
5. Guarda y verifica que aparece en la lista de agentes disponibles.

## Uso

### Flujo rápido

1. Selecciona el agente: elige Code Refactor en Copilot Chat.
2. Prepara el código y contexto: pega o selecciona el fragmento a refactorizar.
3. Indica el motivo y la versión objetivo (p. ej., “modernizar a .NET 8, mejorar testabilidad”).
4. Envía la petición.
5. Revisa la salida:
	- A. Antes (Código original)
	- B. Después (Refactorizado a [lenguaje-versión objetivo])
	- C. Explicación de los cambios (problemas, mejoras, beneficios, riesgos)

> Si falta el motivo o la versión, el agente hará solo una pregunta breve para aclararlo y continuará.

## Formato de salida obligatorio

El agente siempre devuelve tres secciones con estos títulos exactos y en este orden:

### A. Antes (Código original)

Reproduce el código tal cual (solo posibles minimejoras de formato).

### B. Después (Refactorizado a [lenguaje-versión objetivo])

Código modernizado, manteniendo la funcionalidad y aplicando prácticas actuales.
Incluye comentarios donde haya cambios de API, extracción de lógica o patrones.

### C. Explicación de los cambios

- Problemas del código original
- Mejoras aplicadas (refactors, migración de APIs, legibilidad, rendimiento, testabilidad)
- Beneficios obtenidos
- Riesgos o consideraciones (validar con tests, diferencias de versión, nullability, concurrencia, etc.)

## Ejemplos de prompts

🟦 **Migración Java 8 → Java 21**

> Quiero migrar este servicio de Java 8 a Java 21. Motivo: legibilidad y modernización.
> Usa streams y APIs modernas si aportan claridad (sin cambiar la lógica).
> Devuelve Antes / Después / Explicación de los cambios.

```java
[PEGA AQUÍ LA CLASE/MÉTODO]
```

🟩 **Limpieza .NET → .NET 8**

> Refactoriza este controlador de .NET Framework 4.6 a .NET 8.
> Motivo: eliminar duplicidades y dejar listo para tests (DI).
> Mantén el comportamiento y evita dependencias deprecated.

🟧 **Angular 12 → Angular 17**

> Moderniza este componente Angular 12 a Angular 17.
> Motivo: mejorar arquitectura interna, usar OnPush, patrones RxJS actuales y separar responsabilidades.
> Añade comentarios donde cambies APIs obsoletas.

🟨 **Python 2/legacy → Python 3.x**

> Refactoriza este script Python a Python 3.11.
> Motivo: legibilidad y rendimiento en bucles.
> Evita cambios funcionales; sugiere alternativas si detectas I/O bloqueante costoso.

## Consejos de uso

- Define motivo y versión objetivo para un refactor más preciso.
- Si el repo ya tiene patrones/estilo, pide que el agente se alinee usando codebase.
- Para salidas grandes, solicita separación por archivos (con rutas sugeridas) o por módulos.
- Si priorizas rendimiento, dilo explícitamente (p. ej., reducir complejidad y evitar trabajo redundante).
- Si priorizas testabilidad, solicita DI, interfaces y separación de efectos externos (I/O, DB, red).
- Indica frameworks si afectan a la migración (Spring/ASP.NET/Angular…).

## Resolución de problemas

- No indiqué versión objetivo / motivo → El agente hará una pregunta mínima y seguirá.
- El código es muy largo → Divide por fragmentos o pide refactor por módulos.
- Rupturas por framework → Aporta versión y convenciones; adjunta configuración relevante (p. ej., Spring).
- Conflictos con estilos del repo → Pide que consulte codebase para alinear naming y estructura.
- Cambios funcionales no deseados → Reitera “mantener funcionalidad original” y solicita revisión de puntos marcados.

## Seguridad y privacidad

- No compartas credenciales ni datos sensibles reales.
- Valida el resultado con tu suite de tests y revisiones de código (especialmente al migrar versiones).
- Revisa cambios en manejo de errores, nullability y concurrencia al pasar a nuevas APIs.

## Estructura recomendada de carpeta en proyecto

```text
.github/
└─ agents/
	└─ code-refactor/
		├─ code-refactor.agent.md   # Instrucciones del agente para pegar en Copilot
		└─ README.md                # Este documento
```

---

Si quieres, en el siguiente paso te entrego también la carpeta completa con code-refactor.agent.md + README.md en un ZIP listo para descargar e incorporar al repo. ¿Te lo preparo ahora, Roger?
🤖 Code Refactor — Agente de Refactorización y Modernización Multilenguaje
Agente personalizado de GitHub Copilot que refactoriza y moderniza código existente, generando una vista Antes / Después, aplicando buenas prácticas modernas e idiomáticas, y explicando claramente los cambios y sus beneficios. Mantiene la funcionalidad original salvo que se indique lo contrario o sea necesario para corregir errores evidentes.

Índice

#descripción
#características-clave
#lenguajes-y-contextos-soportados
#requisitos-previos
#instalación--configuración-en-github-copilot
#uso
#formato-de-salida-obligatorio
#ejemplos-de-prompts
#consejos-de-uso
#resolución-de-problemas
#seguridad-y-privacidad
#estructura-recomendada-de-carpeta-en-proyecto


Descripción
Code Refactor transforma código legado o desactualizado para mejorar legibilidad, estructura, rendimiento, testabilidad y compatibilidad con versiones modernas (p. ej., Java 21, .NET 8, Angular 17, Python 3.x). El agente:

Analiza el fragmento aportado (selección del editor, archivo activo o código pegado).
Moderniza usando APIs actuales y patrones recomendados (evitando deprecated).
Reduce deuda técnica: duplica menos, simplifica anidaciones, separa responsabilidades.
Devuelve una vista Antes (código original) → Después (refactorizado) → Explicación de los cambios con beneficios y consideraciones.


Objetivo: entregar un refactor claro, mantenible y listo para integrar, priorizando la equivalencia funcional salvo petición o corrección necesaria.


Características clave

🧹 Refactorización estructural: extracción de métodos/clases, separación de responsabilidades, reducción de complejidad.
♻️ Modernización a la versión objetivo (idiomas/idiomas y frameworks) evitando APIs obsoletas.
📐 Buenas prácticas idiomáticas y estilo consistente con el ecosistema.
🧪 Preparación para tests: desacoplo, DI cuando aplique, puntos de extensión.
📝 Explicación clara de cambios, beneficios y riesgos/consideraciones.
🧰 Herramientas: codebase (contexto del repo), search (localización de patrones y referencias internas).


Lenguajes y contextos soportados

Java (incl. migración a Java 21, servicios, repositorios, REST)
.NET (migración a .NET 8, controladores, Minimal APIs, servicios)
Angular (actualización a Angular 17, componentes, servicios, RxJS)
Python 3.x (scripts, módulos, FastAPI/Flask cuando aplique)
TypeScript / JavaScript
PL/SQL (procedimientos, funciones, paquetes)
Cobol (mejora de estructura y legibilidad)


Cuando el proyecto usa un framework (Spring, ASP.NET, Angular…), el agente respeta sus convenciones y ciclos de vida.


Requisitos previos

IDE con GitHub Copilot Chat habilitado (VS Code recomendado).
Agente Code Refactor creado en Agentes Personalizados.
Workspace del proyecto abierto para aprovechar el contexto (codebase).
Tres datos clave para mejores resultados:

Código original,
Motivo principal (legibilidad, rendimiento, deuda técnica, modernización, tests…),
Lenguaje/versión objetivo (p. ej., “Java 21”).




Instalación / Configuración en GitHub Copilot

Abre Copilot Chat en el IDE.
Ve a Agentes (Custom/Personalizados).
Crea un nuevo agente: Code Refactor.
Pega el contenido del archivo code-refactor.agent.md.
Guarda y verifica que aparece en la lista de agentes disponibles.


Uso
Flujo rápido

Selecciona el agente: elige Code Refactor en Copilot Chat.
Prepara el código y contexto: pega o selecciona el fragmento a refactorizar.
Indica el motivo y la versión objetivo (p. ej., “modernizar a .NET 8, mejorar testabilidad”).
Envía la petición.
Revisa la salida:

A. Antes (Código original)
B. Después (Refactorizado a [lenguaje-versión objetivo])
C. Explicación de los cambios (problemas, mejoras, beneficios, riesgos)




Si falta el motivo o la versión, el agente hará solo una pregunta breve para aclararlo y continuará.


Formato de salida obligatorio
El agente siempre devuelve tres secciones con estos títulos exactos y en este orden:


A. Antes (Código original)

Reproduce el código tal cual (solo posibles minimejoras de formato).



B. Después (Refactorizado a [lenguaje-versión objetivo])

Código modernizado, manteniendo la funcionalidad y aplicando prácticas actuales.
Incluye comentarios donde haya cambios de API, extracción de lógica o patrones.



C. Explicación de los cambios

Problemas del código original
Mejoras aplicadas (refactors, migración de APIs, legibilidad, rendimiento, testabilidad)
Beneficios obtenidos
Riesgos o consideraciones (validar con tests, diferencias de versión, nullability, concurrencia, etc.)




Ejemplos de prompts
🟦 Migración Java 8 → Java 21

Quiero migrar este servicio de Java 8 a Java 21. Motivo: legibilidad y modernización.
Usa streams y APIs modernas si aportan claridad (sin cambiar la lógica).
Devuelve Antes / Después / Explicación de los cambios.
[PEGA AQUÍ LA CLASE/MÉTODO]

🟩 Limpieza .NET → .NET 8

Refactoriza este controlador de .NET Framework 4.6 a .NET 8.
Motivo: eliminar duplicidades y dejar listo para tests (DI).
Mantén el comportamiento y evita dependencias deprecated.

🟧 Angular 12 → Angular 17

Moderniza este componente Angular 12 a Angular 17.
Motivo: mejorar arquitectura interna, usar OnPush, patrones RxJS actuales y separar responsabilidades.
Añade comentarios donde cambies APIs obsoletas.

🟨 Python 2/legacy → Python 3.x

Refactoriza este script Python a Python 3.11.
Motivo: legibilidad y rendimiento en bucles.
Evita cambios funcionales; sugiere alternativas si detectas I/O bloqueante costoso.

🟥 PL/SQL (paquete legacy)

Limpia y estructura este paquete PL/SQL: separa responsabilidades, documenta bloques y reduce duplicación.
Motivo: mantenibilidad y preparación para auditoría.
Mantén comportamiento; marca con -- TODO los puntos que dependan de reglas no definidas.

🟪 Cobol (programa batch)

Mejora la legibilidad y la estructura de este Cobol batch, separando secciones lógicas, renombrando campos confusos y eliminando duplicidades.
Motivo: facilitar mantenimiento y pruebas.


Consejos de uso

Define motivo y versión objetivo para un refactor más preciso.
Si el repo ya tiene patrones/estilo, pide que el agente se alinee usando codebase.
Para salidas grandes, solicita separación por archivos (con rutas sugeridas) o por módulos.
Si priorizas rendimiento, dilo explícitamente (p. ej., reducir complejidad y evitar trabajo redundante).
Si priorizas testabilidad, solicita DI, interfaces y separación de efectos externos (I/O, DB, red).
Indica frameworks si afectan a la migración (Spring/ASP.NET/Angular…).


Resolución de problemas

No indiqué versión objetivo / motivo → El agente hará una pregunta mínima y seguirá.
El código es muy largo → Divide por fragmentos o pide refactor por módulos.
Rupturas por framework → Aporta versión y convenciones; adjunta configuración relevante (p. ej., Spring).
Conflictos con estilos del repo → Pide que consulte codebase para alinear naming y estructura.
Cambios funcionales no deseados → Reitera “mantener funcionalidad original” y solicita revisión de puntos marcados.


Seguridad y privacidad

No compartas credenciales ni datos sensibles reales.
Valida el resultado con tu suite de tests y revisiones de código (especialmente al migrar versiones).
Revisa cambios en manejo de errores, nullability y concurrencia al pasar a nuevas APIs.


Estructura recomendada de carpeta en proyecto
Plain Text/.github/└─ agents/   └─ code-refactor/      ├─ code-refactor.agent.md   # Instrucciones del agente para pegar en Copilot      └─ README.md                # Este documentoMostrar más líneas

Si quieres, en el siguiente paso te entrego también la carpeta completa con code-refactor.agent.md + README.md en un ZIP listo para descargar e incorporar al repo. ¿Te lo preparo ahora, Roger?