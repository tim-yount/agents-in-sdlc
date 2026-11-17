---
title: "Lección 1: Instrucciones personalizadas (VS Code)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lección anterior: Requisitos previos][previous-lesson] · [Siguiente lección: Modo de agente →][next-lesson]

El contexto es fundamental cuando trabajas con IA generativa. Si una tarea debe realizarse de una forma concreta o Copilot necesita información previa, asegúrate de que tenga acceso a ella. Los [archivos de instrucciones][instruction-files] permiten proporcionar indicaciones sobre cómo generar el código.

En esta lección:

- explorarás cómo llegan a Copilot el contexto del proyecto, las directrices de programación y los estándares de documentación.
- generarás una primera parte de la capa de datos para el filtrado (una función auxiliar para editoriales) con las instrucciones actuales.
- añadirás un estándar general a `.github/copilot-instructions.md`.
- repetirás el prompt y observarás cómo el código generado sigue el nuevo estándar.
- combinarás los cambios en `main` para que Copilot use las instrucciones actualizadas en la siguiente lección.

> [!CAUTION]
> El código generado puede no seguir todos los estándares. Copilot es probabilístico. El objetivo es observar la tendencia tras actualizar las instrucciones, no obtener siempre un resultado idéntico.

## Archivos de instrucciones

### Escenario

Tailspin Toys tiene varias directrices: la capa de datos necesita pruebas unitarias, la interfaz debe ofrecer un modo oscuro moderno, el código debe incluir comentarios TSDoc y cada archivo debe empezar con un bloque de comentarios que explique su función.

### Instrucciones personalizadas

Las instrucciones personalizadas proporcionan contexto y preferencias a Copilot para que entienda mejor tu estilo y requisitos de programación. Puedes especificar las convenciones de código, bibliotecas y tipos de comentarios que prefieres. Crea instrucciones para todo el repositorio o para tareas y tipos de archivo concretos.

Hay dos tipos de archivos de instrucciones:

- `.github/copilot-instructions.md` es un único archivo que se envía a Copilot en **todas** las solicitudes del repositorio. Debe contener información general del proyecto relevante para la mayoría de las solicitudes de chat o CLI, como la pila tecnológica, una descripción de lo que se está creando, las prácticas recomendadas y otras directrices globales.
- `.github/instructions/*.instructions.md` se puede crear para tareas o tipos de archivo concretos. Permite indicar pautas para lenguajes como TypeScript o Astro, o para tareas como crear un componente de interfaz o un conjunto de pruebas unitarias.

> [!NOTE]
> En un IDE, los archivos de instrucciones solo se usan para generar código en Copilot Chat, no para completar código ni para sugerencias de siguiente edición.
>
> Copilot Chat, Copilot CLI y el agente en la nube usan tanto las instrucciones del repositorio como los archivos `*.instructions.md` con frontmatter `applyTo` al generar código.
>
> Copilot también admite archivos de instrucciones que siguen otros estándares, como AGENTS.md y CLAUDE.md.

### Prácticas recomendadas para gestionar archivos de instrucciones

Crear archivos de instrucciones podría dar lugar a una conversación más amplia de la que cabe en este taller. Sin embargo, los ejemplos del proyecto muestran un enfoque representativo. En general:

- Mantén `copilot-instructions.md` centrado en las directrices del proyecto: una descripción de lo que se está creando, la estructura del proyecto y los estándares globales de programación.
- Usa `*.instructions.md` para dar pautas específicas a tipos de archivo (pruebas unitarias, componentes Astro, capa de datos) o tareas concretas.
- Escribe en lenguaje natural. Procura que las directrices sean claras e incluye ejemplos de cómo debería y no debería ser el código.

No hay una única manera correcta de crear archivos de instrucciones, igual que tampoco hay una sola manera de usar la IA. La experimentación te ayudará a encontrar lo que funciona mejor para tu proyecto.

> [!TIP]
> Todo proyecto que utilice GitHub Copilot puede beneficiarse de una colección sólida de archivos de instrucciones. Mientras exploras los archivos del proyecto, verás que hay instrucciones para distintos tipos de tareas, como [actualizaciones de la interfaz][ui-instructions] y [Astro][astro-instructions].
>
> Copilot también puede ayudarte a generar archivos de instrucciones. Cada interfaz lo ofrece de una forma distinta (por ejemplo, **Configure Chat → Generate Agent Instructions** en VS Code o `/init` en Copilot CLI); la lección de cada interfaz lo explicará cuando corresponda.
>
> ¿Buscas plantillas o un punto de partida? Explora [awesome-copilot][awesome-copilot], un repositorio con archivos de instrucciones, agentes personalizados y otros recursos.

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## Explorar los archivos de instrucciones del proyecto

Dedica un momento a leer los archivos de instrucciones incluidos en este repositorio: hay un archivo principal `copilot-instructions.md` y una colección de archivos `*.instructions.md` para distintas tareas. Ábrelos en el editor o en la interfaz web de GitHub.

1. Abre `.github/copilot-instructions.md` y revisa secciones como **Agent notes**, **Code standards**, **Scripts** y **Repository Structure**, incluida la guía **GitHub Actions Workflows**.
2. Explora `.github/instructions`, donde hay pautas para Astro, Drizzle, pruebas y otras tareas.
3. Abre `.github/instructions/unit-tests.instructions.md` y consulta `applyTo`. En este caso, coincide con archivos de prueba TypeScript como `**/*.test.ts`.
4. Lee las instrucciones para crear pruebas unitarias.
5. Abre `.github/instructions/drizzle.instructions.md` y consulta sus enlaces a otros archivos y ejemplos. Las rutas son relativas al archivo de instrucciones.

> [!NOTE]
> La sección **Code formatting requirements** establece los estándares de programación, pero todavía no exige documentación en el código. Añadirás comentarios TSDoc y encabezados de archivo.

## Crear una rama para los cambios

Sigamos algunas prácticas recomendadas y creemos una rama para estos cambios.

1. Vuelve al Codespace y abre un terminal con <kbd>Control</kbd>+<kbd>`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
2. Crea una rama nueva:

   ```bash
   git checkout -b custom-instructions
   ```

## Usar Copilot Chat antes de actualizar las instrucciones

> [!TIP]
> **Abrir Copilot Chat**
>
> Vuelve al Codespace, abre Copilot Chat y selecciona **New Chat** para iniciar una conversación nueva. El modo y el modelo pueden variar; las instrucciones de cada ejercicio indican cuándo seleccionarlos.

Para observar el efecto de las instrucciones personalizadas, primero envía un prompt con el archivo de instrucciones actual. Más adelante, lo actualizarás y volverás a enviar el mismo prompt para comparar el resultado.

1. Cierra las pestañas abiertas de ejercicios anteriores.
2. Abre `src/lib/publishers.ts` para indicar dónde debe ubicarse la función auxiliar.
3. Selecciona **Agent** en el selector de agentes de la vista Chat para que Copilot pueda aplicar cambios a los archivos.

   ![Captura del selector de agentes en la vista Chat](../../../_images/shared-chat-mode-selector.png)
4. Envía este prompt:

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

5. Copilot explora el proyecto y aplica cambios, a menudo en la función auxiliar y sus pruebas.
6. Observa que la función propuesta tiene tipos y recibe un cliente `db`, siguiendo las convenciones de la capa de datos de `.github/instructions/drizzle.instructions.md`.
7. Observa que el código propuesto **no incluye** comentarios TSDoc ni un encabezado de archivo.

> [!CAUTION]
> Como Copilot es probabilístico, puede que añada comentarios aunque no se lo hayas indicado. No pasa nada: el objetivo es observar la mejora de coherencia después de actualizar las instrucciones.

## Añadir un estándar para todo el repositorio

1. Vuelve a abrir `.github/copilot-instructions.md`.
2. Localiza la sección **Code formatting requirements**, que debería estar cerca de la línea 27. Describe los estándares de programación del proyecto, pero aún no incluye una regla para la documentación en el código; por eso la función auxiliar generada no tenía comentarios.
3. Añade estas líneas de Markdown debajo de los estándares existentes, para indicar a Copilot que añada encabezados de comentarios de archivo y comentarios TSDoc:

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. Guarda el archivo.

> [!TIP]
> Como viste en la lección anterior, los archivos de instrucciones pueden estar en el nivel del repositorio (`.github/copilot-instructions.md`) para ofrecer directrices globales, o ser archivos `*.instructions.md` para lenguajes, tipos de archivo o tareas concretos. El archivo del repositorio es el lugar adecuado para estándares globales, como la regla sobre los comentarios que acabas de añadir.

## Repetir el prompt y observar el cambio

1. Vuelve a Copilot Chat y selecciona **New Chat**.
2. Abre `src/lib/publishers.ts`.
3. Envía el mismo prompt de antes:

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

4. Comprueba que el archivo empieza con un bloque de comentarios parecido a:

   ```typescript
   /**
    * Publisher data-access helpers for the Tailspin Toys Crowd Funding platform.
    * Provides functions to retrieve publisher information from the database.
    */
   ```

5. Comprueba que la función incluye un comentario TSDoc similar a:

   ```typescript
   /**
    * Returns a list of all publishers with their id and name.
    *
    * @param db - The Drizzle database client.
    * @returns A promise that resolves to an array of publisher objects.
    */
   ```

Has indicado a Copilot que siga un estándar nuevo y lo aplique al código que utilizarás en la siguiente lección.

## Confirmar y enviar la rama

1. Abre un terminal nuevo con <kbd>Control</kbd>+<kbd>`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
2. Confirma que las instrucciones actualizadas y los cambios de la función auxiliar estén presentes ejecutando:

   ```bash
   git status
   ```

3. Prepara y confirma las instrucciones y los cambios de la función auxiliar:

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   # If git status shows additional supporting updates (for example tests), add those files too.
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

4. Envía la rama:

   ```bash
   git push -u origin custom-instructions
   ```

## Crear y combinar una solicitud de incorporación de cambios

Con la rama enviada, crea una solicitud de incorporación de cambios y relaciónala con la incidencia sobre los estándares de documentación del backlog. Podrías hacerlo manualmente, pero Copilot puede buscar la incidencia, crear la PR para cerrarla y, después, combinarla.

> [!NOTE]
> Este es el primer ejercicio en el que Copilot realizará acciones en GitHub por ti. La plantilla del proyecto ya conecta las herramientas de GitHub con tu espacio de trabajo, así que no tienes que configurar nada. La primera vez que Copilot use una de ellas, VS Code podría pedirte que inicies sesión en GitHub. Sigue las instrucciones para autorizarlo. En una lección posterior aprenderás cómo funciona esta conexión (Model Context Protocol).

1. Abre Copilot Chat y asegúrate de que esté seleccionado **Agent**.
2. Pulsa <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd> (Windows/Linux) para abrir Copilot Chat.
3. Pide a Copilot que encuentre la incidencia sobre la actualización de los archivos de instrucciones y cree una PR desde la rama actual, indicando que cierra esa incidencia e incluyendo la función auxiliar de editoriales:

   ```plaintext
   Find the issue related to updating the instructions file. Create a new PR from the current branch, highlight that the PR closes that issue, and include that we also added the publishers helper foundation for the upcoming filtering work.
   ```

4. Copilot buscará la incidencia y creará la PR.
5. Si Copilot te pide permiso para realizar acciones de GitHub, revisa el comando y selecciona **Allow** cuando corresponda.
6. Cuando se cree la PR, pídele a Copilot que la combine y que vuelva a `main` en tu entorno local:

   ```plaintext
   Merge the PR into main. Then return to main locally, and pull the latest code so we are up to date.
   ```

7. Si Copilot te pide permiso para realizar acciones de GitHub o ejecutar comandos de shell, revisa el comando y selecciona **Allow** cuando corresponda.

¡Has creado y combinado una PR con ayuda de GitHub Copilot!

## Resumen y siguientes pasos

Has explorado cómo Copilot obtiene contexto de los archivos de instrucciones del proyecto y has usado Copilot Chat en VS Code para:

- enviar un prompt de generación de código y observar el resultado con las instrucciones *existentes*.
- añadir un estándar general al repositorio en `.github/copilot-instructions.md`.
- volver a enviar el mismo prompt y observar cómo el código propuesto sigue el nuevo estándar.
- confirmar los cambios de las instrucciones y la función auxiliar en `main` para que la siguiente lección pueda aprovecharlos.

A continuación, usarás las instrucciones nuevas en [modo de agente][next-lesson] para añadir una funcionalidad.

## Recursos

- [Archivos de instrucciones para personalizar GitHub Copilot][instruction-files]
- [Prácticas recomendadas para crear instrucciones personalizadas][instructions-best-practices]
- [Cinco consejos para redactar mejores instrucciones][copilot-instructions-five-tips]
- [Instrucciones personales para GitHub Copilot][personal-instructions]
- [Awesome Copilot: colección de instrucciones y otros recursos][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[personal-instructions]: https://docs.github.com/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
