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
| [Code Optimizer](../agents/code-optimizer.agent.md) | Perform janitorial tasks on C#/.NET code including cleanup, modernization, and tech debt remediation. |
| [Code Commenter](../agents/code-commenter.agent.md) | Perform janitorial tasks on C#/.NET code including cleanup, modernization, and tech debt remediation. |
| [Code Explainer](../agents/code-explainer.agent.md) | Perform janitorial tasks on C#/.NET code including cleanup, modernization, and tech debt remediation. |
| [Code Refactor](../agents/code-refactor.agent.md) | Perform janitorial tasks on C#/.NET code including cleanup, modernization, and tech debt remediation. |
| [Code Generator](../agents/code-generator.agent.md) | Perform janitorial tasks on C#/.NET code including cleanup, modernization, and tech debt remediation. |
