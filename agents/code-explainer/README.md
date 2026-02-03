# 🤖 Code Explainer — Agente de Explicación Técnica y Funcional Multilenguaje

Agente personalizado de GitHub Copilot que explica de forma estructurada fragmentos de código en múltiples lenguajes (modernos y legacy). Identifica el lenguaje, resume el propósito, detalla el flujo técnico, expone las reglas de negocio, destaca errores/malas prácticas y riesgos, y genera una versión comentada inline del código. Soporta modo desarrollador y modo analista/negocio.

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

Code Explainer interpreta y explica fragmentos de código (selección del editor, archivo activo o texto pegado en el chat) en múltiples lenguajes: Java, .NET, JavaScript/Angular, Python, entre otros.

A partir del código recibido, el agente:

- Detecta el lenguaje y el tipo de artefacto (método, clase, procedimiento, trigger, componente…).
- Genera una Descripción general (propósito, datos clave y efectos).
- Produce una Explicación técnica (flujo, estructuras, dependencias, patrones, implicaciones).
- Produce una Explicación funcional (reglas de negocio, procesos, resultados).
- Añade Explicación por líneas/bloques con referencias de líneas (Lx–Ly) cuando sea posible.
- Señala Errores y malas prácticas y Riesgos y puntos críticos.
- Devuelve una versión del código comentada inline (sin modificar la lógica).

**Objetivo:** ofrecer una comprensión clara y accionable del código para desarrolladores y analistas/negocio, con foco en claridad, estructura y utilidad práctica.

## Características clave

- 🔎 Detección de lenguaje y contexto del fragmento.
- 🧠 Explicación técnica y funcional en secciones separadas.
- 🧩 Desglose por líneas/bloques con referencias (Lx–Ly), cuando sea posible.
- 🧯 Detección de errores/malas prácticas y señalamiento de riesgos técnicos/funcionales.
- 📝 Código comentado inline en la convención del lenguaje (sin cambiar la lógica).
- 🧰 Herramientas: codebase, search (cuando el entorno del IDE las expone).
- 🧭 Modos de explicación: desarrollador / negocio (o ambos por defecto).
- 🗣️ Tono didáctico y profesional con terminología adecuada al público.

## Lenguajes y contextos soportados

- Java, C#/.NET, JavaScript/TypeScript (incl. Angular), Python
- Otros lenguajes: aplica convenciones de comentarios y explicación estándar.

> El agente no refactoriza ni modifica el comportamiento; su función es explicar y documentar el fragmento.

## Requisitos previos

- IDE con GitHub Copilot Chat habilitado.
- Agente Code Explainer creado en Agentes Personalizados.
- Workspace del proyecto abierto para aprovechar contexto (codebase).

## Instalación / Configuración en GitHub Copilot

1. Abre Copilot Chat en el IDE.
2. Ve a Agentes (Custom/Personalizados).
3. Crea un nuevo agente llamado Code Explainer.
4. Pega el contenido del archivo `code-explainer.agent.md`.
5. Guarda y verifica que aparece en la lista de agentes disponibles.

## Uso

### Flujo rápido

1. Selecciona el agente: elige Code Explainer en Copilot Chat.
2. Prepara el fragmento: selecciona o pega el código (método, clase, trigger, script…).
	- Si te interesa una parte concreta, indica el rango (p. ej., L35–L80).
3. Indica el modo (opcional):
	- “modo desarrollador (técnico)” o “modo negocio (funcional)”.
4. Envía la petición: añade cualquier pregunta o contexto adicional que quieras que el agente tenga en cuenta.
5. Revisa el resultado:
	- Descripción general → Explicación técnica → Explicación funcional → Explicación por bloques → Errores/Malas prácticas → Riesgos → Código comentado inline.

## Formato de salida obligatorio

El agente SIEMPRE devuelve las siguientes secciones con estos títulos exactos (y en este orden):

1. **Descripción general del código**
2. **Explicación técnica (para desarrolladores)**
3. **Explicación funcional (para analista/negocio)**
4. **Explicación por líneas/bloques**
5. **Errores y malas prácticas**
6. **Riesgos y puntos críticos**
7. **Código comentado inline**

> Si el usuario solicita solo modo técnico, se mantienen 1 y 2 (y el resto si se piden).
> Si solicita solo modo negocio, se mantienen 1 y 3 (y el resto si se piden).

## Ejemplos de prompts

🟦 **Java (servicio Spring)**

> Explica este servicio Java en modo desarrollador. Identifica el flujo, dependencias (repositorios/servicios), manejo de excepciones y posibles riesgos de rendimiento o seguridad. Añade explicación por bloques con líneas.

```java
[PEGA AQUÍ LA CLASE O MÉTODO]
```

🟩 **.NET (controlador ASP.NET Core)**

> En modo negocio, explica qué casos de uso implementa este controlador C# y qué reglas de validación aplica. Añade una versión con comentarios inline.

```csharp
[PEGA AQUÍ EL CONTROLADOR]
```

🟧 **Angular (componente + template)**

> Explica el flujo entre componente y template, la gestión de estado, suscripciones RxJS y validaciones en formularios. Indica riesgos (rendimiento, XSS con innerHTML, etc.).

```typescript
[PEGA AQUÍ EL COMPONENTE/TEMPLATE]
```

🟨 **Python (script o módulo)**

> Dame una explicación técnica paso a paso de este módulo Python, cubriendo estructura, funciones clave, errores/malas prácticas y riesgos. Incluye versión comentada inline.

```python
[CÓDIGO AQUÍ]
```

## Consejos de uso

- Incluye contexto suficiente (framework, propósito del módulo) si no es evidente.
- Si el archivo es muy grande, selecciona el bloque relevante o indica rangos.
- Elige el modo (técnico o negocio) según tu audiencia.
- Pide foco en riesgos específicos si te interesa (p. ej., “evalúa riesgos de concurrencia y rendimiento”).
- Si quieres solo la versión comentada, dilo explícitamente.

## Resolución de problemas

- No detecta el lenguaje → Indícalo manualmente en el prompt.
- No hay líneas en el editor → Pega el fragmento y el agente referenciará bloques sin numeración.
- Explicación muy general → Aporta más contexto o pregunta por áreas concretas (seguridad, rendimiento, negocio).
- Fragmento ambiguo o incompleto → El agente indicará límites de interpretación y pedirá la mínima aclaración necesaria.
- Demasiado largo → Divide por secciones o solicita enfoque en “flujo principal” + “riesgos”.

## Seguridad y privacidad

- No pegues credenciales ni datos personales sensibles en el chat.
- Revisa que los comentarios inline no expongan información interna que no deba publicarse.
- El agente no ejecuta el código: valida las conclusiones con tu equipo y pruebas.

## Estructura recomendada de carpeta en proyecto

```text
.github/
└─ agents/
	└─ code-explainer/
		├─ code-explainer.agent.md   # Instrucciones del agente para pegar en Copilot
		└─ README.md                 # Este documento
```

---

¿Quieres que te genere también los archivos (code-explainer.agent.md + README.md) en una carpeta lista para descargar (.zip) y subir a tu repo? Puedo prepararlo ahora mismo.
🤖 Code Explainer — Agente de Explicación Técnica y Funcional Multilenguaje
Agente personalizado de GitHub Copilot que explica de forma estructurada fragmentos de código en múltiples lenguajes (modernos y legacy). Identifica el lenguaje, resume el propósito, detalla el flujo técnico, expone las reglas de negocio, destaca errores/malas prácticas y riesgos, y genera una versión comentada inline del código. Soporta modo desarrollador y modo analista/negocio.

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
Code Explainer interpreta y explica fragmentos de código (selección del editor, archivo activo o texto pegado en el chat) en múltiples lenguajes: Java, .NET, JavaScript/Angular, Python, PL/SQL, Cobol, Oracle Forms/Reports, entre otros.
A partir del código recibido, el agente:

Detecta el lenguaje y el tipo de artefacto (método, clase, procedimiento, trigger, componente…).
Genera una Descripción general (propósito, datos clave y efectos).
Produce una Explicación técnica (flujo, estructuras, dependencias, patrones, implicaciones).
Produce una Explicación funcional (reglas de negocio, procesos, resultados).
Añade Explicación por líneas/bloques con referencias de líneas (Lx–Ly) cuando sea posible.
Señala Errores y malas prácticas y Riesgos y puntos críticos.
Devuelve una versión del código comentada inline (sin modificar la lógica).


Objetivo: ofrecer una comprensión clara y accionable del código para desarrolladores y analistas/negocio, con foco en claridad, estructura y utilidad práctica.


Características clave

🔎 Detección de lenguaje y contexto del fragmento.
🧠 Explicación técnica y funcional en secciones separadas.
🧩 Desglose por líneas/bloques con referencias (Lx–Ly), cuando sea posible.
🧯 Detección de errores/malas prácticas y señalamiento de riesgos técnicos/funcionales.
📝 Código comentado inline en la convención del lenguaje (sin cambiar la lógica).
🧰 Herramientas: codebase, search (cuando el entorno del IDE las expone).
🧭 Modos de explicación: desarrollador / negocio (o ambos por defecto).
🗣️ Tono didáctico y profesional con terminología adecuada al público.


Lenguajes y contextos soportados

Java, C#/.NET, JavaScript/TypeScript (incl. Angular), Python
PL/SQL / SQL, Cobol, Oracle Forms/Reports
Otros lenguajes: aplica convenciones de comentarios y explicación estándar.


El agente no refactoriza ni modifica el comportamiento; su función es explicar y documentar el fragmento.


Requisitos previos

IDE con GitHub Copilot Chat habilitado (VS Code recomendado).
Agente Code Explainer creado en Agentes Personalizados.
Workspace del proyecto abierto para aprovechar contexto (codebase).


Instalación / Configuración en GitHub Copilot

Abre Copilot Chat en el IDE.
Ve a Agentes (Custom/Personalizados).
Crea un nuevo agente llamado Code Explainer.
Pega el contenido del archivo code-explainer.agent.md.
Guarda y verifica que aparece en la lista de agentes disponibles.


Uso
Flujo rápido

Selecciona el agente: elige Code Explainer en Copilot Chat.
Prepara el fragmento: selecciona o pega el código (método, clase, trigger, script…).

Si te interesa una parte concreta, indica el rango (p. ej., L35–L80).


Indica el modo (opcional):

“modo desarrollador (técnico)” o “modo negocio (funcional)”.


Envía la petición: añade cualquier pregunta o contexto adicional que quieras que el agente tenga en cuenta.
Revisa el resultado:

Descripción general → Explicación técnica → Explicación funcional → Explicación por bloques → Errores/Malas prácticas → Riesgos → Código comentado inline.




Formato de salida obligatorio
El agente SIEMPRE devuelve las siguientes secciones con estos títulos exactos (y en este orden):

Descripción general del código
Explicación técnica (para desarrolladores)
Explicación funcional (para analista/negocio)
Explicación por líneas/bloques
Errores y malas prácticas
Riesgos y puntos críticos
Código comentado inline


Si el usuario solicita solo modo técnico, se mantienen 1 y 2 (y el resto si se piden).
Si solicita solo modo negocio, se mantienen 1 y 3 (y el resto si se piden).


Ejemplos de prompts
🟦 Java (servicio Spring)

Explica este servicio Java en modo desarrollador. Identifica el flujo, dependencias (repositorios/servicios), manejo de excepciones y posibles riesgos de rendimiento o seguridad. Añade explicación por bloques con líneas.
[PEGA AQUÍ LA CLASE O MÉTODO]

🟩 .NET (controlador ASP.NET Core)

En modo negocio, explica qué casos de uso implementa este controlador C# y qué reglas de validación aplica. Añade una versión con comentarios inline.
[PEGA AQUÍ EL CONTROLADOR]

🟧 Angular (componente + template)

Explica el flujo entre componente y template, la gestión de estado, suscripciones RxJS y validaciones en formularios. Indica riesgos (rendimiento, XSS con innerHTML, etc.).
[PEGA AQUÍ EL COMPONENTE/TEMPLATE]

🟨 Python (script o módulo)

Dame una explicación técnica paso a paso de este módulo Python, cubriendo estructura, funciones clave, errores/malas prácticas y riesgos. Incluye versión comentada inline.
[CÓDIGO AQUÍ]

🟥 PL/SQL (procedimiento)

Explica este procedimiento PL/SQL: entradas, proceso (queries/updates), reglas de negocio y posibles riesgos (bloqueos, errores silenciosos, inyección). Añade explicación por bloques con rango de líneas.
[CÓDIGO AQUÍ]

🟪 Cobol (programa batch)

En modo negocio, explica el proceso por fases (lectura, transformación, escritura), las validaciones y salidas. Luego dame una versión comentada del código original (sin cambiar la lógica).
[CÓDIGO AQUÍ]

🧩 Rango específico del archivo actual

Explica solo de la L20 a la L65 del archivo actual. Dame Descripción general, Explicación técnica, por bloques con líneas, Errores/Malas prácticas, Riesgos y Código comentado inline.
(Selecciona el rango o indícalo en el prompt)


Consejos de uso

Incluye contexto suficiente (framework, propósito del módulo) si no es evidente.
Si el archivo es muy grande, selecciona el bloque relevante o indica rangos.
Elige el modo (técnico o negocio) según tu audiencia.
Pide foco en riesgos específicos si te interesa (p. ej., “evalúa riesgos de concurrencia y rendimiento”).
Si quieres solo la versión comentada, dilo explícitamente.


Resolución de problemas

No detecta el lenguaje → Indícalo manualmente en el prompt.
No hay líneas en el editor → Pega el fragmento y el agente referenciará bloques sin numeración.
Explicación muy general → Aporta más contexto o pregunta por áreas concretas (seguridad, rendimiento, negocio).
Fragmento ambiguo o incompleto → El agente indicará límites de interpretación y pedirá la mínima aclaración necesaria.
Demasiado largo → Divide por secciones o solicita enfoque en “flujo principal” + “riesgos”.


Seguridad y privacidad

No pegues credenciales ni datos personales sensibles en el chat.
Revisa que los comentarios inline no expongan información interna que no deba publicarse.
El agente no ejecuta el código: valida las conclusiones con tu equipo y pruebas.


Estructura recomendada de carpeta en proyecto
Plain Text/.github/└─ agents/   └─ code-explainer/      ├─ code-explainer.agent.md   # Instrucciones del agente para pegar en Copilot      └─ README.md                 # Este documentoMostrar más líneas

¿Quieres que te genere también los archivos (code-explainer.agent.md + README.md) en una carpeta lista para descargar (.zip) y subir a tu repo? Puedo prepararlo ahora mismo.