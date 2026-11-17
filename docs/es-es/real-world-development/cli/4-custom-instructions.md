---
title: "Lección 4: Guiar a Copilot con instrucciones personalizadas"
description: "Explora las instrucciones del repositorio, añade un estándar de documentación y aplícalo al código de filtrado."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

El contexto es fundamental cuando trabajas con IA generativa. Si una tarea debe realizarse de una forma concreta, conviene proporcionar a Copilot las indicaciones pertinentes. Los [archivos de instrucciones][instruction-files] describen no solo *qué* código quieres, sino también *cómo* debe estructurarse. Ahora que has creado el filtrado, explorarás las instrucciones utilizadas por Copilot, añadirás un estándar de documentación y lo aplicarás al código.

En esta lección:

- explorarás cómo llegan al agente las instrucciones del repositorio y las instrucciones específicas para determinadas rutas.
- actualizarás el archivo de instrucciones para que se sigan los estándares de programación.
- comprobarás el efecto de los archivos de instrucciones en el código.

## Escenario

Tailspin Toys tiene directrices y requisitos para el desarrollo:

- Los comentarios deben explicar la intención y las decisiones que no sean obvias, no repetir el código.
- Las funciones exportadas de `db/` y `src/lib/` deben documentar con TSDoc/JSDoc su finalidad, sus parámetros y sus valores devueltos; también deben documentar el argumento `db` inyectable cuando exista.
- Los componentes Astro reutilizables deben documentar sus contratos `Props`, y los comentarios deben mantenerse actualizados cuando cambie el código relacionado.
- Se deben conservar las directrices de formato y lint existentes.

Con los archivos de instrucciones, proporcionarás a Copilot la información necesaria para que realice las tareas de acuerdo con estas prácticas.

## Archivos de instrucciones

Las instrucciones personalizadas proporcionan contexto y preferencias a Copilot para que entienda mejor tu estilo de programación. Puedes especificar convenciones de código, bibliotecas y los comentarios que prefieres. Crea instrucciones para todo el repositorio o para tipos de archivo y tareas concretos.

Hay dos tipos de archivos de instrucciones:

- `.github/copilot-instructions.md` es un único archivo que se envía a Copilot en todas las solicitudes del repositorio. Debe contener indicaciones generales pertinentes para la mayoría de las solicitudes.
- `.github/instructions/*.instructions.md` contiene directrices para lenguajes, tipos de archivo o tareas concretos.

> [!NOTE]
> Los formatos admitidos varían según el entorno. Consulta la [referencia de compatibilidad con instrucciones personalizadas][custom-instructions-support] antes de depender de un formato específico.

## Explorar los archivos de instrucciones del proyecto

El proyecto incluye varios archivos de instrucciones. Revísalos antes de hacer cambios para comprobar qué orientación recibe Copilot.

1. Vuelve a tu Codespace.
2. En el editor de Codespaces (no en el terminal), abre `.github/copilot-instructions.md`.
3. Lee la descripción breve del proyecto y las directrices de programación. Se aplican a todas las interacciones con Copilot en este repositorio.
4. Explora los archivos de la carpeta `.github/instructions`. Hay instrucciones para Astro, la capa de datos Drizzle, las pruebas y otros ámbitos.
5. Abre `.github/instructions/unit-tests.instructions.md` y consulta el campo `applyTo`, que define a qué archivos se aplica el patrón.
6. Abre `.github/instructions/drizzle.instructions.md` y consulta sus enlaces a otros archivos de instrucciones y ejemplos del proyecto.

## Actualizar las instrucciones del equipo

Los archivos actuales son un buen punto de partida, pero falta una directriz. Modifica `copilot-instructions.md` para pedir comentarios TSDoc en el nuevo código TypeScript.

1. Localiza la sección **Code formatting guidance**, que debería estar cerca de la línea 35.
2. Añade el siguiente elemento al final de la lista:

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

El archivo se guardará automáticamente.

## Aplicar las instrucciones actualizadas

Copilot CLI carga las instrucciones del repositorio al iniciar una conversación. Después de guardar el cambio, sal y reanuda la conversación de filtrado para que Copilot aplique las instrucciones nuevas sin perder el contexto de la funcionalidad.

1. Si la conversación de filtrado sigue abierta, escribe `/exit`. Copilot CLI guarda las conversaciones automáticamente.
2. Desde la raíz del repositorio, en la rama `game-filters-cli`, reanuda la conversación:

   ```bash
   copilot --resume
   ```

   Si se te solicita, selecciona la conversación de filtrado y confirma que está seleccionada la rama `game-filters-cli`.
3. Pide a Copilot que aplique las nuevas directrices:

   ```plaintext
   We just updated our instructions and code guidance. Can you please update the code you generated to match that guidance?
   ```

4. Escribe `/diff` y revisa los archivos TypeScript modificados. Observa los comentarios TSDoc generados y confirma que describen el código correctamente.

## Resumen y siguientes pasos

Has explorado cómo Copilot utiliza los archivos de instrucciones y has aplicado un estándar nuevo a la funcionalidad. En concreto:

- exploraste cómo llegan al agente las instrucciones del repositorio y las específicas para determinadas rutas.
- actualizaste el archivo de instrucciones para seguir los estándares de programación.
- comprobaste el efecto de los archivos de instrucciones en el código.

A continuación, [personalizarás y ejecutarás la habilidad reutilizable quality-checks][next-lesson] para comprobar de forma coherente el lint y las pruebas.

## Recursos

- [Añadir instrucciones personalizadas para Copilot CLI][instruction-files]
- [Compatibilidad con instrucciones personalizadas][custom-instructions-support]
- [Prácticas recomendadas para crear instrucciones personalizadas][instructions-best-practices]
- [Awesome Copilot: colección de instrucciones y otros recursos][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
