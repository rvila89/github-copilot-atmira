# 🤖 Code Generator — Agente de Generación de Código Multilenguaje

Agente personalizado de GitHub Copilot que genera código listo para integrar a partir de una descripción funcional (inputs, outputs, reglas de negocio, restricciones técnicas), aplicando buenas prácticas idiomáticas, estructura clara y manejo adecuado de errores. Cuando la información es insuficiente o ambigua, pide aclaraciones mínimas antes de comprometer decisiones importantes.

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

Code Generator crea componentes y módulos listos para integrar en diversos stacks (Java 21, .NET 8, Angular, Python, etc.) a partir de una especificación funcional clara.

El agente:

- Solicita y valida Inputs, Outputs, Reglas de negocio y Restricciones técnicas.
- Genera código con estructura limpia, modular, mantenible y alineado con el estilo del lenguaje.
- Añade comentarios útiles (intención, reglas, decisiones de diseño) y manejo de errores cuando corresponde.
- Evita suposiciones críticas: si falta contexto, pregunta y utiliza placeholders explícitos solo cuando la información no es esencial.

**Objetivo:** entregar código funcional y comentado, con decisiones de diseño explícitas y preparado para integrarse en proyectos reales, priorizando la claridad y la mantenibilidad.

## Características clave

- 🏗️ Generación de código a partir de descripciones funcionales completas.
- 🧠 Buenas prácticas idiomáticas y estructura modular por defecto.
- 🧾 Documentación inline adecuada al lenguaje (JavaDoc, XML, docstrings…).
- 🧰 Uso opcional de codebase/search para alinearse con el repositorio (nombres, patrones, estilos existentes).
- 🧩 Diseño razonado: explica brevemente la estructura y señala puntos configurables.
- 🛑 Sin suposiciones peligrosas: si faltan datos críticos, pide aclaraciones mínimas.
- 🧭 Tono profesional y conciso, con foco en entregables listos para integrar.

## Lenguajes y contextos soportados

- Java 21 (p. ej., Spring Boot, REST, servicios, repositorios)
- .NET 8 (ASP.NET Core, Minimal APIs, controladores)
- Angular 17 (componentes, servicios, modelos, interceptores)
- Python (FastAPI, Flask, utilidades, servicios)
- Otros lenguajes: se aplican principios generales de claridad, modularidad y coherencia.

> Cuando el proyecto usa un framework concreto (Spring, ASP.NET, Angular…), el agente respeta sus convenciones y ciclos de vida típicos.

## Requisitos previos

- IDE con GitHub Copilot Chat activo.
- Agente Code Generator creado en la sección de Agentes Personalizados.
- Workspace del proyecto abierto para que el agente pueda usar el contexto del repositorio.

## Instalación / Configuración en GitHub Copilot

1. Abre Copilot Chat en el IDE.
2. Ve a Agentes (Custom/Personalizados).
3. Crea un agente y asígnale el nombre: Code Generator.
4. Pega el contenido del archivo `code-generator.agent.md`.
5. Guarda y verifica que aparece en tu lista de agentes disponibles.

## Uso

### Flujo rápido

1. Selecciona el agente: en Copilot Chat, elige Code Generator.
2. Prepara la especificación: define Inputs, Outputs, Reglas, Restricciones y Lenguaje/versión.
3. Envía la petición: pega la descripción funcional y cualquier contexto de repo relevante (nombres de entidades, rutas, etc.).
4. Itera si es necesario: si faltan datos, el agente hará preguntas puntuales.
5. Recibe el resultado:
	- Código completo (uno o varios archivos, con bloque etiquetado por lenguaje).
	- Comentarios explicando intención, parámetros y decisiones clave.
	- Explicación breve del diseño elegido.

## Formato de salida obligatorio

El agente siempre respeta estas reglas de salida:

### Estructura de respuesta (texto / Markdown)

- Responde en Markdown legible con títulos y listas si procede.

### Bloques de código

- Todo el código va en bloques Markdown con el lenguaje indicado.
- Para varios archivos, separa por subtítulos, p. ej.:

```markdown
### File: src/main/java/com/example/App.java
### File: src/main/resources/application.yml
```

### Si pides “solo código” o “sin explicaciones”

- Devuelve únicamente los bloques de código necesarios, sin texto adicional.

### Si pides explicación + código

- Primero una explicación breve (estructura, decisiones, supuestos).
- Después el/los bloque(s) de código.

### Marcadores y placeholders

- Cuando falte información no crítica, utiliza marcadores explícitos:

```java
// TODO: completar regla de negocio X
```
```sql
-- TODO: ajustar consulta Y según requisitos finales
```

### Resúmenes finales (opcionales)

- Para soluciones extensas, añade un resumen de clases/módulos generados (fuera de los bloques de código).

## Ejemplos de prompts

🟦 **Java 21 (Spring Boot — Servicio y controlador)**

> Necesito un servicio REST para crear pedidos en Java 21 + Spring Boot.
> Inputs: CreateOrderRequest { customerId, items[], paymentMethod }.
> Outputs: CreateOrderResponse { orderId, status } con HTTP 201.
> Reglas: validar stock, calcular impuestos (IVA 21%), rechazar si pago inválido.
> Restricciones: logs mínimos, excepciones controladas, idempotencia por clientToken.
> Genera controlador + servicio + DTOs y comenta la lógica clave.

🟩 **.NET 8 (Minimal APIs)**

> Crea Minimal APIs en .NET 8 para alta/listado de “clientes”.
> Input POST: CustomerCreate { name, email } con validación de email.
> Output: 201 + objeto creado.
> Restricciones: manejar errores con ProblemDetails, separar capa de servicio, inyección de dependencias.

🟧 **Angular 17 (Componente + Servicio + Modelo)**

> Genera un componente Angular 17 para buscar productos con paginación.
> Incluye servicio HTTP, interfaz Product, manejo de loading y errores, y template accesible (ARIA).
> Restricciones: no usar librerías extra, OnPush, RxJS con catchError.

🟨 **Python (FastAPI)**

> En FastAPI, crea un endpoint /payments/refund que reciba {paymentId, amount}.
> Reglas: validar que amount > 0 y amount <= originalAmount.
> Restricciones: pydantic models, manejo de errores 400/404/409, docstrings PEP257, función de servicio separada.

## Consejos de uso

- Define versiones y frameworks (Java 21, .NET 8, Angular 17…) para obtener código idiomático.
- Aporta modelos/DTOs existentes o nombres de entidades para alinear el diseño.
- Especifica restricciones (rendimiento, seguridad, observabilidad, estándares internos).
- Indica si prefieres “solo código” o “explicación + código”.
- Para salidas grandes, pide separación por archivos y rutas destino.
- Si el repo ya tiene patrones/estilo, indica que se alinee usando codebase.
- Usa placeholders cuando un detalle no esté cerrado; concreta luego en una iteración.

## Resolución de problemas

- Falta de información / ambigüedad → El agente hará preguntas mínimas. Responde en el mismo hilo.
- Salida demasiado extensa → Solicita dividir por archivos o módulos.
- Necesitas otro enfoque de diseño → Indica tu preferencia (DDD, hexagonal, MVC, CQRS…).
- Integración con código existente → Proporciona rutas/clases relevantes para mantener coherencia.
- Errores de compilación por entorno → Especifica versión exacta y dependencias esperadas.

## Seguridad y privacidad

- No pegues credenciales ni datos sensibles reales (usa valores ficticios).
- Señala si hay requisitos de auditoría, trazabilidad, enmascaramiento o cumplimiento (p. ej., GDPR).
- Revisa cuidadosamente el código de validaciones y manejo de errores antes de producción.

## Estructura recomendada de carpeta en proyecto

```text
.github/
└─ agents/
	└─ code-generator.agent.md   # Instrucciones del agente para pegar en Copilot
```