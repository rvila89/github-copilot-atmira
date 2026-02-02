# 🤖 Agentes Personalizados

Los agentes personalizados permiten especializar GitHub Copilot para que actúe como un colaborador experto en tareas concretas.
Este sistema hace posible que equipos y organizaciones creen agentes adaptados a su forma de trabajar.

Un agente personalizado es un archivo *.agent.md que define:

- La persona del agente (rol, especialidad, tono, ámbito de trabajo).
- Las instrucciones sobre cómo debe actuar ante diferentes tareas.
- Los comandos, herramientas o flujos que puede ejecutar.
- Los límites y reglas que debe respetar (por ejemplo, qué carpetas no tocar).

## ¿Cómo utilizar los agentes personalizados?

**Para instalar:**
1. Descarga el archivo *.agent.md.
2. Añádelo a tu repositorio dentro de la carpeta .github/agents/

**Activar y usar un agente personalizado**
1. Abre el panel de Copilot Chat.
2. Selecciona el agente instalado desde el menú desplegable.
3. Interactúa con él directamente.

| Agent | Description |
| ----- | ----------- |
| [Code Optimizer](../agents/code-optimizer.agent.md) | Agente especializado en análisis y refactorización de código multi‑lenguaje, aplicando principios de Clean Code, SOLID y OWASP, para detectar code smells, bugs y vulnerabilidades, devolviendo una versión más limpia, legible y mantenible junto con un breve informe de hallazgos |
| [Code Commenter](../agents/code-commenter.agent.md) | Agente especializado en generar comentarios y documentación técnica a partir de código fuente, usando el estándar de comentarios de cada lenguaje para crear documentación clara, profesional y enfocada en la intención del código. |
| [Code Explainer](../agents/code-explainer.agent.md) | Agente experto en explicar de forma estructurada fragmentos de código en múltiples lenguajes (modernos y legacy), tanto a nivel técnico como funcional, identificando el lenguaje, resumiendo el propósito, detallando el flujo, las reglas de negocio, los riesgos y generando versiones comentadas del código. |
| [Code Refactor](../agents/code-refactor.agent.md) | Asistente experto en refactorización y modernización de código que genera una vista antes/después, aplica buenas prácticas modernas y explica claramente los cambios y beneficios. |
| [Code Generator](../agents/code-generator.agent.md) | Agente especializado en generación automática de código a partir de especificaciones, plantillas o ejemplos, facilitando la creación rápida y consistente de componentes, módulos o servicios en múltiples lenguajes y frameworks. |