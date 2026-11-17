---
title: "Lección 2: Agente de GitHub Copilot en la nube"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Muchas organizaciones tienen deuda técnica: incidencias de seguridad pendientes, código heredado que necesita actualizaciones o funcionalidades que llevan tiempo en el backlog. El agente de GitHub Copilot en la nube puede actualizar código y añadir funcionalidades de forma autónoma. Cuando termina, abre una PR para que una persona revise el resultado. Así puedes delegar tareas y centrarte en el trabajo de mayor alcance.

En esta lección explorarás cómo personalizar el entorno, asegurar las operaciones, definir incidencias acotadas y asignar trabajo al agente.

## Escenario

Tailspin Toys tiene dos tareas. La primera consiste en añadir comentarios TSDoc a las funciones exportadas. La segunda es añadir juegos relacionados a la página de detalles de cada juego para que el equipo de diseño pueda probar la experiencia. Son tareas que pueden quedar relegadas y que se pueden delegar para que el agente trabaje de forma asíncrona.

## Acerca del agente de GitHub Copilot en la nube

[El agente de GitHub Copilot en la nube][copilot-agents] puede trabajar en segundo plano de forma parecida a un desarrollador. Puedes, por ejemplo, [asignarle una incidencia de GitHub][assign-issue]. El agente crea una PR preliminar para registrar el progreso, configura un entorno y comienza el trabajo. Puedes consultar la sesión mientras se ejecuta o después. Cuando la solución esté lista para revisar, te mencionará en la PR.

## La importancia de unas instrucciones bien acotadas

GitHub Copilot no elimina la necesidad de pensar ni de definir el alcance. Incluso las tareas aparentemente sencillas pueden ser complejas. Ten en cuenta las [prácticas recomendadas para acotar tareas del agente en la nube][cloud-agent-best-practices]. Trátalo como un compañero de programación con IA: trabaja por etapas, aprende, experimenta y adapta el enfoque.

## Instrucciones personalizadas en este repositorio

Antes de asignar trabajo, consulta los archivos de instrucciones que ya existen:

- `.github/copilot-instructions.md`: revisa **Code standards**, especialmente las convenciones TypeScript y los comentarios TSDoc.
- `.github/instructions/unit-tests.instructions.md`: fíjate en `applyTo`, que aplica estas instrucciones a archivos `**/*.test.ts`.

Al asignar la incidencia `Code lacks documentation`, comprueba si la PR incluye comentarios TSDoc, convenciones TypeScript y encabezados de comentarios. Estas indicaciones proceden de los archivos de instrucciones.

## Configurar el entorno de desarrollo

El agente usa [GitHub Actions][github-actions] como entorno. Puedes personalizarlo con el flujo de configuración `.github/workflows/copilot-setup-steps.yml`, que se ejecuta antes de que el agente empiece a trabajar. El flujo de este taller ya instala Node.js y las dependencias, Playwright Chromium y configura la base de datos SQLite.

El flujo tiene un trabajo llamado `copilot-setup-steps`. El activador `workflow_dispatch` permite ejecutarlo manualmente desde la pestaña **Actions** para comprobar que funciona.

## Asignar la tarea de documentación

1. Abre tu repositorio en github.com y selecciona la pestaña **Issues**.
2. Selecciona **New issue** y, después, **Blank issue**.
3. Usa `Code lacks documentation` como título y esta descripción:

   ```plaintext
   Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
   ```

4. Selecciona **Create** y, en el panel derecho, **Assign to Copilot**.
5. En el cuadro de asignación, selecciona **Assign**.
6. Abre la pestaña **Pull Requests** y revisa la nueva PR. Puede tener un título parecido a `[WIP]: Code lacks documentation`.
7. Espera a que aparezca la lista de tareas del agente y selecciona **View session** para observar su trabajo.

> [!NOTE]
> La lista puede tardar varios minutos en aparecer mientras Copilot prepara el entorno, analiza el proyecto y determina un enfoque.

El agente trabaja de forma asíncrona. Mientras tanto, puedes asignarle otra tarea.

## Añadir una sección de juegos relacionados

1. En github.com, crea otra incidencia con el título `Show related games on the game details page`.
2. Usa esta descripción:

   ```markdown
   We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
   ```

3. Selecciona **Create** y asigna la incidencia al agente con **Assign to Copilot** y **Assign**.

Cuando el agente empiece a trabajar, aparecerá 👀 en el primer comentario de la incidencia. No es necesario supervisarlo continuamente; revisa su trabajo cuando termine.

## Resumen y siguientes pasos

Has explorado el agente de GitHub Copilot en la nube y cómo asignarle incidencias para que trabaje de forma asíncrona. También has revisado la configuración del entorno y has asignado tareas de documentación y de juegos relacionados.

A continuación, crearás y usarás [agentes personalizados][next-lesson]. El agente en la nube también puede usar servidores MCP y las instrucciones personalizadas que has explorado.

## Recursos

- [Acerca del agente de Copilot en la nube][copilot-agents]
- [Asignar incidencias de GitHub a Copilot][assign-issue]
- [Prácticas recomendadas para el flujo de configuración del agente][cloud-agent-best-practices]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
