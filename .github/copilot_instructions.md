Las siguientes instrucciones solo deben aplicarse al realizar una revisión de código.

## Actualizaciones de README

- [ ] El nuevo fichero debe añadirse a `docs/README.<type>.md`.

## Guía de archivos de agentes

**Aplicar solo a archivos que terminan en `.agent.md`**

- [ ] El agente tiene front matter de Markdown.
- [ ] El agente tiene un campo `description`.
- [ ] El campo `description` no está vacío.
- [ ] El nombre del fichero está en minúsculas, con palabras separadas por guiones.
- [ ] Fomentar el uso de `tools`, aunque no es obligatorio.
- [ ] Recomendar encarecidamente usar `model` para especificar el modelo para el que el agente estçe optimizado.
- [ ] Recomendar encarecidamente usar `name` para establecer el nombre del agente.

## Guía de archivos prompts

**Aplicar solo a archivos que terminan en `.prompt.md`**

- [ ] El prompt tiene front matter de Markdown.
- [ ] El prompt tiene un campo `agent` especificado como `agent`, `ask` o `Plan`.
- [ ] El prompt tiene un campo `description`.
- [ ] El campo `description` no está vacío.
- [ ] El nombre del fichero está en minúsculas, con palabras separadas por guiones.
- [ ] Fomentar el uso de `tools`, aunque no es obligatorio.
- [ ] Recomendar encarecidamente usar `model` para especificar el modelo para el que el prompt esté optimizado.
- [ ] Recomendar encarecidamente usar `name` para establecer el nombre del prompt.

## Guía de archivos de instrucciones

**Aplicar solo a archivos que terminan en `.instructions.md`**

- [ ] La instrucción tiene front matter de Markdown.
- [ ] La instrucción tiene un campo `description`.
- [ ] El campo `description` no está vacío.
- [ ] El nombre del fichero está en minúsculas, con palabras separadas por guiones.
- [ ] La instrucción incluye un campo `applyTo` que especifica el/los ficheros a los que aplican las instrucciones. Si se desean especificar múltiples rutas de fichero, deberían formatearse como `'**.js, **.ts'`.

## Guía de skills del agente

**Aplicar solo a carpetas en el directorio `skills/`**

- [ ] La carpeta de la skill contiene un fichero `SKILL.md`.
- [ ] El `SKILL.md` tiene front matter de Markdown.
- [ ] El `SKILL.md` tiene un campo `name`.
- [ ] El valor del campo `name` está en minúsculas y con palabras separadas por guiones.
- [ ] El campo `name` coincide con el nombre de la carpeta.
- [ ] El `SKILL.md` tiene un campo `description`.
- [ ] El campo `description` no está vacío, tiene al menos 10 caracteres y como máximo 1024.
- [ ] El valor del campo `description` está envuelto entre comillas simples.
- [ ] El nombre de la carpeta está en minúsculas, con palabras separadas por guiones.
- [ ] Cualquier asset incluido (scripts, plantillas, ficheros de datos) está referenciado en las instrucciones del `SKILL.md`.
- [ ] Los assets incluidos tienen un tamaño razonable (menos de 5MB por fichero).
