# 🤖 Code Commenter — Agente de Comentarios y Documentación Técnica Multilenguaje

Agente personalizado de GitHub Copilot diseñado para generar comentarios y documentación técnica directamente sobre el código, siguiendo los estándares oficiales de cada lenguaje (JavaDoc, XML comments, docstrings, etc.) y produciendo documentación clara, estructurada y alineada con la intención del código.

**Autor(es):** ai-tools  
**Equipo/Área responsable:** atmira 
**Fecha de creación:** [AAAA-MM-DD]  
**Última actualización:** [AAAA-MM-DD]  
**Equipos o proyectos que lo utilizan:**  
- [Proyecto/Equipo 1]  

## Índice

- [Descripción](#descripción)
- [Características clave](#características-clave)
- [Lenguajes y formatos soportados](#lenguajes-y-formatos-soportados)
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

Code Commenter genera automáticamente comentarios y documentación técnica a partir de código fuente en múltiples lenguajes.
Detecta la estructura del código (clases, métodos, interfaces, parámetros, valores de retorno, reglas de negocio visibles, validaciones, dependencias, etc.) y añade comentarios adaptados al estándar de documentación propio de cada lenguaje:

- JavaDoc (Java)
- XML Comments (C#)
- Docstrings PEP257 (Python)
- Comentarios estándar PL/SQL
- Comentarios Cobol
- Comentarios C-like para otros lenguajes

Opcionalmente puede generar una plantilla completa de documentación técnica, basada en el código.

## Características clave

- 📘 Generación automática de comentarios estándar (JavaDoc, XML, docstrings, PL/SQL…)
- ✍️ Comentarios de alto nivel, bajo nivel o ambos
- 🧠 Documentación orientada a intención del código (no solo descripción literal)
- 🧩 Plantillas de documentación técnica listas para usar (opcional)
- 🔎 Identificación automática del lenguaje si no se indica
- 🛡️ Respeto total de la lógica del código (no se modifica)
- 🧰 Herramientas disponibles: codebase, search (si el IDE las expone)
- 🧭 Tono profesional, didáctico y claro

## Lenguajes y formatos soportados

**Lenguajes principales (máxima cobertura):**

- Java → JavaDoc
- C# / .NET → XML Comments
- Python → Docstrings (PEP257)

**Lenguajes adicionales:**

- JavaScript / TypeScript
- Go
- C / C++
- Bash
- Otros lenguajes → comentarios estándar de estilo C-like

> Si el lenguaje no es evidente, el agente intentará deducirlo o solicitará aclaración.

## Requisitos previos

- Tener GitHub Copilot Chat habilitado en el IDE
- Crear el agente manualmente en la sección de Agentes Personalizados
- Workspace del proyecto abierto para proporcionar suficiente contexto

## Instalación / Configuración en GitHub Copilot

1. Abre Copilot Chat.
2. Ve a la sección Agentes personalizados.
3. Crea un nuevo agente con nombre: Code Commenter.
4. Copia y pega el contenido del archivo `code-commenter.agent.md`.
5. Guarda y confirma que el agente aparece disponible.

## Uso

### Flujo rápido

1. Selecciona el agente Code Commenter en Copilot Chat.
2. Copia o selecciona el fragmento de código.
3. Indica el nivel de documentación deseado:
	- “comentarios de alto nivel”
	- “comentarios detallados por método”
	- “genera plantilla técnica además”
4. El agente devolverá:
	- Código documentado → (siempre)
	- Plantilla técnica → (si la pides)

## Formato de salida obligatorio

El agente SIEMPRE devuelve:

1. **Código documentado**
	- El mismo código que enviaste.
	- Con comentarios generados en el formato estándar del lenguaje.
	- Sin modificar la lógica.
	- Con ligeras mejoras de formato si ayudan a la legibilidad.

2. **Plantilla de documentación técnica (opcional)**
	- Solo si la solicitas explícitamente.
	- Incluye secciones como:
	  - Resumen del módulo/clase
	  - Lista de funciones/métodos con parámetros y retornos
	  - Dependencias relevantes
	  - Consideraciones especiales
	  - Posibles excepciones
	  - Precondiciones/postcondiciones

## Ejemplos de prompts

🟦 **Java (JavaDoc)**

> Añade comentarios JavaDoc de alto y bajo nivel a esta clase de servicio Java, explicando su propósito, cada método, parámetros y valores de retorno.

```java
[PEGA AQUÍ EL CÓDIGO]
```

🟩 **C# (.NET)**

> Genera XML comments para este controlador en C#. Incluye resumen de la clase, descripción de cada acción y parámetros.

```csharp
[CÓDIGO AQUÍ]
```

🟧 **Python**

> Añade docstrings a estas funciones de Python. Incluye parámetro, retorno y propósito. Después genera una plantilla de documentación técnica.

```python
[CÓDIGO AQUÍ]
```

## Consejos de uso

- Aporta contexto cuando sea necesario (módulo, propósito, framework)
- Si el archivo es muy grande, selecciona por partes
- Indica el nivel de detalle que deseas
- Para documentación completa, pide explícitamente: “Genera también una plantilla de documentación técnica.”
- Si el lenguaje no es claro, indícalo
- Si quieres técnica más extensa, añade: “Incluye decisiones de diseño y dependencias internas.”

## Resolución de problemas

- El agente no detecta el lenguaje: Indícalo manualmente.
- Comentarios demasiado genéricos: Añade contexto adicional en el prompt.
- Documento muy largo: Divide el archivo en secciones o métodos.
- Código con errores de sintaxis: El agente documentará lo posible, pero no corregirá la lógica.

## Seguridad y privacidad

- No incluyas credenciales en código.
- Los comentarios pueden hacer visibles reglas internas del negocio, revisa antes de subir a repositorios públicos.
- El agente no ejecuta código; valida cualquier fragmento sensible antes de publicarlo.

## Estructura recomendada de carpeta en proyecto

```text
.github/
└─ agents/
	└─ code-commenter.agent.md   # Archivo para pegar en Copilot
```