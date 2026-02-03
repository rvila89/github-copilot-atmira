# 🤖 Code Optimizer — Agente de Revisión y Refactorización Multilenguaje

Agente personalizado de GitHub Copilot que analiza y optimiza fragmentos de código en múltiples lenguajes, aplicando Clean Code, SOLID y OWASP. Entrega siempre un informe breve de hallazgos, el código reformateado y optimizado y comentarios sobre los cambios clave, manteniendo la lógica de negocio salvo petición explícita o corrección de errores evidentes.

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

Code Optimizer analiza automáticamente fragmentos de código en múltiples lenguajes (Java, .NET, JavaScript/Angular, Cobol, PL/SQL, Python, entre otros) para detectar problemas evidentes de calidad, mantenibilidad y seguridad. Identifica code smells, posibles bugs, vulnerabilidades típicas (alineadas con OWASP cuando aplique), complejidad o redundancia innecesaria y malas prácticas de estilo.

A partir de ese análisis, genera una versión reformateada y optimizada del código, respetando la lógica de negocio, aplicando convenciones de estilo del lenguaje y entregando un informe de hallazgos y comentarios explicando los cambios clave realizados.

## Características clave

- 🔍 Análisis de calidad, riesgos y vulnerabilidades OWASP comunes.
- 🧹 Refactorización y formateo según guías de estilo del lenguaje (p. ej., PEP8 en Python).
- 🧠 Explicaciones técnicas concisas de los cambios e impacto (legibilidad, rendimiento, seguridad y mantenibilidad).
- 🛡️ Respeto de la lógica de negocio (no se crean reglas nuevas salvo petición explícita o para corregir errores evidentes).
- 🧭 Enfoque profesional y preciso, con alternativas justificadas cuando aplique.
- 🧰 Herramientas: codebase, search (cuando el entorno de Copilot las expone en el IDE).

## Lenguajes y contextos soportados

- Java, C#/.NET, JavaScript/TypeScript (incl. Angular), Python
- PL/SQL, SQL
- Cobol (legacy)
- Otros lenguajes: se aplican principios generales de claridad, modularidad, seguridad y buenas prácticas.

> Nota: En proyectos con frameworks (Spring, ASP.NET, Angular, etc.), se respetan convenciones y ciclos de vida estándar.

## Requisitos previos

- IDE con GitHub Copilot Chat habilitado.
- Agente Code Optimizer creado en la sección de agentes personalizados de Copilot Chat (ver siguiente sección).
- Recomendado: abrir el workspace del proyecto para que el agente pueda aprovechar el contexto del código (archivo actual, selección, etc.).

## Instalación / Configuración en GitHub Copilot

1. Abre Copilot Chat en el IDE.
2. Ve a Agentes (Custom/Personalizados).
3. Crea un nuevo agente y asígnale el nombre: Code Optimizer.
4. Pega el markdown del agente (el fichero `code-optimizer.agent.md` que acompaña a este README).
5. Guarda y verifica que el agente aparece en la lista de agentes disponibles.

## Uso

### Flujo rápido

1. Selecciona el agente: Abre Copilot Chat y elige Code Optimizer.
2. Prepara el código: Añade, copia o selecciona el fragmento a analizar (método, clase, script, procedimiento, componente…); incluye contexto relevante (imports, firma, variables clave).
3. Indica la necesidade de optimizar el código seleccionado mediante el prompt y añade instrucciones adicionales si lo consideras necesario.
4. Revisa el resultado: El agente devolverá Informe → Código optimizado → Comentarios. Valida el resultado y decide si seguir iterando en la respuesta, integrar los cambios que apliquen o descartar la opción.

## Formato de salida obligatorio

El agente siempre devuelve tres secciones en este orden y con estos títulos exactos:

1. **Informe breve de problemas encontrados**: Lista de hallazgos con severidad baja / media / alta y breve explicación.
2. **Código reformateado y optimizado**: Un único bloque con el código completo, manteniendo la equivalencia funcional salvo correcciones de errores obvios (en cuyo caso se indicará en la sección 3).
3. **Comentarios sobre los cambios clave**: Explicación de refactors, mejoras de estilo, simplificaciones y correcciones (impacto en legibilidad, rendimiento, seguridad y mantenibilidad).

---

## Ejemplos de prompts

**Servicio Java (Spring)**

Analiza y optimiza este servicio Java. Reduce complejidad ciclomática, mejora legibilidad y detecta posibles bugs o vulnerabilidades OWASP. Mantén la lógica de negocio.

[PEGA AQUÍ LA CLASE O MÉTODO]

**Componente Angular**

Optimiza este componente Angular. Enfócate en separación de responsabilidades, manejo seguro de inputs y rendimiento de plantillas. Devuélveme informe, código optimizado y comentarios.

[PEGA AQUÍ EL COMPONENTE Y/O TEMPLATE]

**Script Python**

Limpia y refactoriza este script Python siguiendo PEP8. Reduce anidación con guard clauses, elimina duplicidades y señala posibles bugs. No cambies la lógica salvo correcciones obvias.

[PEGA AQUÍ EL SCRIPT]

**Método C# (.NET)**

Analiza este método C# y aplica SOLID cuando aplique. Propón nombres más descriptivos, extrae métodos si es necesario y verifica posibles vulnerabilidades al manejar entradas externas.

[PEGA AQUÍ EL MÉTODO]

---

## Consejos de uso

- Incluye contexto suficiente: imports, firmas, tipos y dependencias relevantes.
- Especifica restricciones: “no cambies la lógica”, “máxima compatibilidad”, “prioriza seguridad/rendimiento”.
- Divide archivos grandes: si el código es muy extenso, procesa por partes o indica rutas/archivos clave.
- Declara el framework: si aplica (Spring, ASP.NET, Angular…), el agente ajustará convenciones.
- Indica el lenguaje si no es obvio por la sintaxis.
- Pide foco OWASP para que priorice sanitización, validaciones y riesgos típicos.

---

## Resolución de problemas

- No aparecen las tres secciones: Repite la solicitud indicando “usa el formato de salida obligatorio”.
- Lenguaje no detectado: Indícalo explícitamente en el prompt.
- Código demasiado largo: Divide en fragmentos o solicita que trabaje por módulos/archivos.
- Rupturas por framework: Indica el framework y versión, o adjunta el contexto (p. ej., configuración de Spring/DI).
- Falsos positivos OWASP: Proporciona detalles de cómo se validan/sanitizan entradas más arriba en la pila.

---

## Seguridad y privacidad

- No pegues credenciales ni secretos. Enmascara valores sensibles.
- Revisa los cambios de seguridad sugeridos (p. ej., parametrización SQL, validación de entradas).
- El agente no ejecuta el código; valida funcionalmente con tu suite de tests y revisiones de código.

---

## Estructura recomendada de carpeta en proyecto
```text              
/.github/
└─ agents/
  └─ code-optimizer.agent.md   # Instrucciones del agente para pegar en Copilo
```