---
title: "Lección 5: Iterar sobre el trabajo de GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lección anterior: Gestionar agentes][previous-lesson] |
|:--|

## Revisar el trabajo

Durante este taller has colaborado con GitHub Copilot en varias tareas para mejorar la experiencia y añadir funcionalidades: documentar el código, implementar juegos relacionados y crear modos de alto contraste y claro. Revisarás los cambios y, si hace falta, enviarás indicaciones para mejorarlos.

### Escenario

Como se ha destacado en varias ocasiones, los fundamentos del diseño de software y DevOps no cambian al añadir IA generativa. Siempre debemos revisar el código generado y seguir el proceso habitual de DevOps. Con esto en mente, revisaremos las sugerencias de GitHub Copilot para documentar el código, crear la funcionalidad de juegos relacionados y añadir las funciones de accesibilidad antes de activar la revisión del resto del equipo.

## Seguridad y agente en la nube

El agente en la nube trabaja de forma asíncrona y sin supervisión directa. Para mantener la seguridad:

- Copilot tiene acceso de lectura al repositorio y acceso de escritura **solo** a la rama en la que trabaja.
- El agente se ejecuta en GitHub Actions dentro de un entorno independiente y temporal.
- Una persona debe aprobar los flujos de trabajo de GitHub Actions antes de ejecutarlos.
- [El acceso a recursos externos está limitado de forma predeterminada][agent-firewall], incluidos los servidores MCP.

## Revisar la documentación generada

Empecemos por la primera solicitud de incorporación de cambios (PR) creada por el agente en la nube de GitHub Copilot, que añade documentación al código. Para ello, usarás la interfaz estándar de PR de GitHub.com.

> [!NOTE]
> Es posible que veas un aviso de que Copilot está bloqueado por un firewall. Es normal: el acceso a recursos externos, incluidos los servidores MCP, está limitado de forma predeterminada. Puedes [configurar o desactivar el firewall del agente en la nube][agent-firewall].

1. Vuelve a tu repositorio en github.com.
2. Selecciona **Pull Requests** para abrir la lista de solicitudes de incorporación de cambios.
3. Abre la solicitud titulada algo parecido a **Add missing documentation** o con un título más descriptivo.

> [!NOTE]
> Si Copilot todavía está trabajando, la solicitud tendrá la etiqueta **[WIP]**. Espera a que termine; puede tardar unos minutos. Mientras tanto, puedes descansar o repasar lo aprendido.

4. Cuando la solicitud esté lista, selecciona la pestaña **Files changed** y revisa los cambios.

   ![Pestaña Files changed](../../../_images/shared-pr-files-changed.png)

5. Explora el código actualizado, que incluirá los nuevos comentarios TSDoc y otra documentación. Los cambios concretos pueden variar.

   Al revisar los cambios, busca comentarios TSDoc, convenciones de TypeScript y encabezados de comentarios. Estas indicaciones proceden de los archivos de instrucciones personalizados que revisaste al principio de la Lección 2.

6. Cuando hayas revisado las actualizaciones y todo parezca correcto, vuelve a la pestaña **Conversation** y desplázate hacia abajo.
7. Deberías ver un indicador de que hay flujos de trabajo pendientes de aprobación.
8. Si hay flujos pendientes, selecciona **Approve and run workflows**.

   ![Aprobar y ejecutar flujos de trabajo](../../../_images/shared-approve-workflows.png)

9. Los flujos de trabajo deberían aparecer en la sección de comprobaciones de la solicitud. Si todo va bien, las comprobaciones del proyecto para la única aplicación Astro se completarán correctamente. Esto puede tardar unos minutos.

## Solicitar cambios a GitHub Copilot

Trabajar con Copilot en una PR no es una interacción unidireccional. Puedes mencionar a Copilot en comentarios de la PR, como harías con cualquier otra persona del equipo, o en comentarios en línea del código. Copilot verá estos comentarios e iniciará otra sesión para resolverlos. Como los resultados no son deterministas, no hay una frase única que debas usar. Algunas ideas de cambios que podrías pedirle:

- Añadir encabezados de comentarios que describan cada archivo.
- Añadir comentarios TSDoc a archivos TypeScript y Astro.
- Crear un README que describa la estructura de la aplicación Astro.

1. Añade un comentario que solicite un cambio en la documentación generada y mencione a **@copilot**, como mencionarías a cualquier usuario. Puedes usar una de las ideas anteriores o pedir otro cambio que quieras ver en el código.
2. Selecciona **View Session** para observar el trabajo de Copilot. Fíjate en que inicia una sesión nueva para realizar las actualizaciones.
3. Puedes seleccionar **Back to pull request** para volver a la solicitud.

   ![Volver a la solicitud de incorporación de cambios](../../../_images/ex7-back-to-pr.png)

4. Cuando Copilot haya terminado, verás un nuevo commit en la solicitud.
5. Selecciona la pestaña **Files changed** para revisar los cambios.

Puedes seguir iterando hasta que estés conforme. Después, marca la PR como lista para revisión y combínala.

![Opción para marcar una PR como lista para revisión](../../../_images/ex7-ready-for-review.png)

## Revisar la funcionalidad de juegos relacionados

1. Vuelve a tu repositorio en GitHub.com.
2. Selecciona la pestaña **Pull Requests**.
3. Selecciona la solicitud titulada algo parecido a **Show related games on the game details page** o con un título más descriptivo.
4. Selecciona la pestaña **Files changed** para revisar el código generado.
5. Cuando hayas revisado las actualizaciones y todo parezca correcto, vuelve a la pestaña **Conversation** y desplázate hacia abajo.
6. Deberías ver un indicador de que hay flujos de trabajo pendientes de aprobación.
7. Si hay flujos pendientes, selecciona **Approve and run workflows**.

   ![Aprobar y ejecutar flujos de trabajo](../../../_images/shared-approve-workflows.png)

8. Los flujos de trabajo deberían aparecer en la sección de comprobaciones de la solicitud. Si todo va bien, las comprobaciones del proyecto para la única aplicación Astro se completarán correctamente. Esto puede tardar unos minutos.
9. **Opcional:** puedes cambiar a esta rama en tu Codespace para probar manualmente la funcionalidad de juegos relacionados. Abre un terminal en el Codespace y ejecuta estos comandos (sustituye `<branch-name>` por el nombre de la rama creada por Copilot, por ejemplo, **copilot/fix-8**):

   ```bash
   git fetch origin
   git checkout <branch-name>
   ```

¡Copilot ha creado la funcionalidad de juegos relacionados! Como antes, puedes seguir iterando con el agente en la nube mediante comentarios nuevos en la pestaña **Conversation**. Por ejemplo, podrías pedirle que ajuste cuántos juegos relacionados se muestran o que añada encabezados de comentarios y comentarios TSDoc (recuerda que esta tarea se asignó **antes** de actualizar las instrucciones personalizadas). Copilot verá esos comentarios e iniciará otra sesión.

## Revisar las funciones de accesibilidad

Revisa la PR del modo de alto contraste. Debe incluir también el modo claro que solicitaste desde Mission Control.

1. Vuelve a tu repositorio en GitHub.com.
2. Selecciona la pestaña **Pull Requests**.
3. Selecciona la solicitud titulada algo parecido a **Add high contrast mode to website** o con un título más descriptivo.

> [!NOTE]
> Si Copilot todavía está trabajando, la solicitud tendrá la etiqueta **[WIP]**. Espera a que termine; puede tardar unos minutos.

4. Selecciona la pestaña **Files changed** para revisar el código generado.
5. Revisa la implementación. Presta atención a:
   - los controles para cambiar de modo.
   - el uso del almacenamiento local para conservar las preferencias.
   - los cambios de CSS para el alto contraste y el modo claro.
   - los atributos de accesibilidad, la navegación con teclado y las etiquetas ARIA.
   - el código JavaScript o TypeScript que controla el cambio de modo.
6. Cuando hayas revisado las actualizaciones y todo parezca correcto, vuelve a la pestaña **Conversation** y desplázate hacia abajo.
7. Deberías ver un indicador de que hay flujos de trabajo pendientes de aprobación.
8. Si hay flujos pendientes, selecciona **Approve and run workflows**.

   ![Aprobar y ejecutar flujos de trabajo](../../../_images/shared-approve-workflows.png)

9. Los flujos de trabajo deberían aparecer en la sección de comprobaciones de la solicitud. Si todo va bien, las comprobaciones del proyecto para la única aplicación Astro se completarán correctamente. Esto puede tardar unos minutos.
10. **Opcional:** puedes cambiar a esta rama en tu Codespace para probar manualmente las funciones de accesibilidad. Abre un terminal en el Codespace y ejecuta estos comandos (sustituye `<branch-name>` por el nombre de la rama creada por Copilot):

   ```bash
   git fetch origin
   git checkout <branch-name>
   ```

   Inicia la aplicación y prueba los modos de alto contraste y claro en el navegador. Comprueba que las preferencias persisten al recargar la página.

Si detectas problemas de accesibilidad, menciona a **@copilot** en un comentario y solicita los cambios pertinentes.

## Ejercicio opcional: seguir delegando

El agente en la nube resulta útil para trabajar en tareas reales del backlog mientras te ocupas de otras cosas. Crea más incidencias y asígnaselas a Copilot. Por ejemplo:

- Crear un formulario de interés para patrocinadores en la página de detalles del juego.
- Implementar paginación en la página de juegos.
- Añadir validación de entradas y manejo de errores a las funciones de acceso a datos.

## Resumen

Has completado el recorrido del agente en la nube. En estas lecciones:

- revisaste los archivos de instrucciones del repositorio y su efecto en el agente.
- asignaste incidencias al agente y observaste cómo configuraba el entorno, planificaba y trabajaba de forma asíncrona.
- creaste y usaste un agente personalizado de accesibilidad para los modos de alto contraste y claro.
- usaste la página de agentes de Copilot para supervisar y dirigir la sesión.
- revisaste las PR del agente y le pediste cambios con comentarios a **@copilot**.

## Revisión y siguientes pasos

Has terminado el recorrido del agente en la nube. Los otros recorridos complementan lo que has practicado:

- 🖥️ **[Recorrido de VS Code](../../vscode/)**: explora el modo de agente de Copilot Chat y la integración de MCP en el IDE.
- 💻 **[Recorrido de CLI](../../cli/)**: entrega dos cambios revisados desde el terminal con Plan, Autopilot, habilidades de agente, un agente de QA, MCP de Playwright, Agent Merge y delegación opcional al agente en la nube.

En tu propio repositorio, prueba estas ideas:

- Asigna al agente una incidencia de refactorización o cobertura de pruebas.
- Crea un agente personalizado para otro ámbito.
- Configura `copilot-setup-steps.yml` para otra pila tecnológica.

## Recursos

- [GitHub Copilot][github-copilot]
- [Acerca de los agentes de Copilot][copilot-agents]
- [Asignar incidencias de GitHub a Copilot][assign-issue]
- [Prácticas recomendadas para el flujo de configuración del agente][cloud-agent-best-practices]
- [Configurar el firewall del agente en la nube][agent-firewall]

---

| [← Lección anterior: Gestionar agentes][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall

[previous-lesson]: ../4-managing-agents/
