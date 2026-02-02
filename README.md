# 🤖 Atmira GitHub Copilot

Bienvenidos al respositorio corporativo para la **gestión, organización y escalado del uso de GitHub Copilot** en los IDEs de la compañía.
Este repositorio centraliza **agentes, prompts, instrucciones, skills, guias y buenás prácticas** con el objetivo de maximizar el impacto de la IA en los flujos de trabajo de ingeniería de tod@s l@s soci@s de la companía.

## 🚀 Objetivo del repositorio
Este proyecto forma parte de la iniciativa estratégica de la compañía para:

- 👉 Estandarizar el uso de **GitHub Copilot** en todos los equipos de de la compañía
- 👉 Habilitar collecciones reutilizables de **prompts, agentes, skills e instrucciones**
- 👉 Compartir conocimiento y acelerar el onboarding en el uso de IA generativa
- 👉 Adaptar herramientas y configuraciones de Copilot al perfil profesional de cada soci@

## 🧩 Colecciones de IA
- **👉 [Agentes](docs/README.agents.md)** - Colección de agentes especializados para distintos contextos
- **👉 [Instructions](docs/README.instructions.md)** - Estándares de codificación integrales y mejores prácticas que se aplican a patrones de archivos específicos o proyectos completos. Proporcionan a Copilot conteexto persistente sobre el proyecto, herramientas, estándares y frameworks. Estas instrucciones permiten que Copilot entienda cómo debe trabajar en todo el repositorio, sin repetir información en cada prompt
- **👉 [Prompts](docs/README.prompts.md)** - Colección de prompts listos para usar en GitHub Copilot Chat que permiten ahorrar tiempo y agregar contexto específico en interacciones concretas del chat
- **👉 [Skills](docs/README.skills.md)** - Conjunto de Agent Skills, una nueva funcionalidad que permite añadir scripts e instrucciones que Copilot detecta automáticamente y utiliza para tareas avanzadas

## 🔧 ¿Cómo se usa?

### 🤖 Agentes
GitHub Copilot permite invocar agentes personalizados definidos en archivos .agent.md al utilizar la herramienta de GitHub Copilot Chat. Al crear un nuevo agente personalizado, aparecerá dentro del listado de agentes seleccionables en la ventanta del chat

### 🎯 Prompts
Puedes invocar prompts del repositorio usando el comando `/` dentro de GitHub Copilot Chat:

```plaintext
/example-prompt create-readme
```

### 📋 Instructions
Las instrucciones se aplican automáticamente a los archivos según sus patrones y ofrecen orientación contextual sobre estándares de codificación, frameworks y buenas prácticas.
Pueden ser:

**Globales del repositorio**: .github/copilot-instructions.md
**Específicas por ruta**: .github/instructions/*.instructions.md

## 📖 Estructura de repositorio
Esta estructura toma como referencia repositorios oficiales de GitHub Copilot como github/awesome-copilot que organizan contenido modularmente

```plaintext
├── prompts/          # Tareas específicas (.prompt.md)
├── instructions/     # Estándares y buenas prácticas (.instructions.md)
├── agents/           # Agentes personalizados (.agent.md)
└── skills/           # Capacidades para los agentes para tareas específicas
```

## 🤝 Contribución
Este repositorio está vivo y se nutre de los aportes de todos los soci@s. Si quieres contribuir:

Crea una rama descriptiva (feature/, fix/, docs/)
Aporta nuevos agentes, prompts o skills
Abre un Pull Request siguiendo la plantilla

📁 Ver guía de contribución: ./CONTRIBUTING.md

## 📄 Licencia
Este repositorio es de uso interno de la compañía.
Consulta más información: ./LICENSE