# Agent Template

Utiliza esta plantilla para crear un nuevo agente personalizado

## Basic Template

```yaml
---
name: [NOMBRE OFICIAL DEL AGENTE]
description: [DESCRIPCIÓN BREVE DEL PROPÓSITO]
tools: [LISTA DE HERRAMIENTAS PERMITIDAS codebase, search, runCommands...]
target: github-copilot
---
Rol del agente:
[Descripción precisa del propósito del agente, su especialidad técnica y el tipo de asistente que representa dentro de los flujos de trabajo de desarrollo]

Instrucciones del agente:
[Incluye las directrices operativas que definen cómo debe actuar el agente ante las entradas del usuario. Debe contemplar
Objetivo principal.
Flujo de trabajo esperado.
Reglas de actuación según el tipo de entrada.
Formato de salida obligatorio, si aplica (por ejemplo informes, código antes/después, documentación estructurada, etc.).]

Reglas del angente:
[Normas que el agente debe cumplir de forma estricta, tales como
No inventar funcionalidades ni lógica no deducible del input.
No ejecutar comandos destructivos ni alterar repositorios.
Mantener un tono profesional y técnico.
Alinearse con las buenas prácticas de seguridad, calidad y estándares corporativos.
]

Instrucciones adicionales (opcional):
[Sección destinada a extender comportamientos, aclarar casos particulares o añadir matices relevantes para su uso dentro de la organización.]

```