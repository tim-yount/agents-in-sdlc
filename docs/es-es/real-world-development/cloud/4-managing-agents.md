---
title: "Lección 4: Supervisar y gestionar agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

En las lecciones anteriores asignaste tres tareas al agente de GitHub Copilot en la nube, centradas en mejorar la experiencia y añadir funcionalidad. Aunque el agente trabaja de forma autónoma y asíncrona, es importante supervisar las tareas.

Puedes gestionar las tareas con varias herramientas, incluida la [página de agentes][agents-page] de GitHub.com. Desde Mission Control puedes ver las tareas de los agentes que tienen PR abiertas, consultar las acciones realizadas y dirigir las sesiones que siguen en curso.

En esta lección:

- explorarás la página de agentes para supervisar las tareas.
- dirigirás una sesión activa para solicitar otra funcionalidad.

## Escenario

Después de asignar al agente la implementación del modo de alto contraste, el equipo decide añadir también un modo claro. Como el trabajo ya incluye cambios de estilo y controles de modo, pedirás al agente que incluya esta función.

## Revisar las tareas del agente en la nube de Copilot

Veamos el estado actual de todas las tareas asignadas al agente en la nube de Copilot.

1. Ve a la [página de agentes de Copilot](https://github.com/copilot/agents).
2. Observa la lista de tareas en el panel principal y en el panel izquierdo. Deberías ver las tareas que asignaste a Copilot, entre ellas:
   - actualizar la documentación del código.
   - generar API para modificar juegos.
   - añadir un modo de alto contraste al sitio web.
3. Selecciona una de las tareas en curso y revisa las acciones que ha realizado Copilot. Pueden incluir:
   - obtener el código del repositorio.
   - crear el entorno de trabajo de Copilot.
   - configurar servidores MCP.
   - realizar distintos pasos para completar la tarea asignada.

> [!NOTE]
> Las acciones que aparecen dependen del estado y del enfoque de la tarea.

4. Observa también el panel de solicitud de incorporación de cambios (PR) que aparece a la derecha. Desde ahí puedes ver la PR y los archivos modificados para supervisar el trabajo.

## Dirigir el agente en la nube

Ahora pedirás al agente que añada un modo claro mientras trabaja en el modo de alto contraste.

1. Selecciona la sesión relacionada con el modo de alto contraste. El título exacto dependerá del nombre que le haya dado Copilot y del estado del trabajo.

   ![Sesión de accesibilidad en Mission Control](../../../_images/ex6-accessibility-session.png)

2. Observa la sesión durante unos minutos, hasta que indique que ha terminado de configurar el entorno y ha empezado a trabajar. Lo sabrás cuando empiecen a aparecer mensajes como los que se muestran a continuación.
3. En el cuadro **Steer active session while Copilot is working**, escribe este prompt:

   ```plaintext
   While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
   ```

   ![Tarea del agente en la nube en la página de agentes, con el cuadro para dirigir la sesión activa resaltado](../../../_images/ex6-steer-cloud-agent-task.png)

4. Pulsa <kbd>Enter</kbd> para enviar el prompt.
5. Observa cómo Copilot confirma que ha recibido el prompt y lo incorpora a su flujo de trabajo.

## Dejar que Copilot trabaje

Copilot incorporará la nueva solicitud cuando termine el paso en curso. El proceso puede tardar varios minutos; puedes aprovechar ese tiempo para repasar lo aprendido.

## Resumen y siguientes pasos

Esta lección ha explorado la página de agentes de Copilot, el centro desde el que puedes supervisar y dirigir las tareas del agente en la nube. Puedes realizar un seguimiento de las tareas activas y completadas, revisar el trabajo y redirigir una sesión en curso para ajustar su alcance o proporcionar más indicaciones.

Has explorado estos conceptos:

- usar Mission Control y la página de agentes para supervisar las tareas del agente en la nube.
- redirigir una sesión en curso para solicitar funcionalidades adicionales.

Mientras Copilot termina su trabajo en las funciones de accesibilidad, puedes pasar a [iterar sobre las solicitudes de incorporación de cambios creadas por Copilot][next-lesson].

## Recursos

- [Página de agentes de Copilot][agents-page]
- [Acerca de los agentes personalizados][custom-agents]

---

| [← Lección anterior: Agentes personalizados][previous-lesson] | [Siguiente lección: Iterar sobre el trabajo de Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
