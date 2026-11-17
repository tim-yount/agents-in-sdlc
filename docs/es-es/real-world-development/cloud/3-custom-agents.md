---
title: "Lección 3: Agentes personalizados"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## ¿Qué son los agentes personalizados?

Los [agentes personalizados][custom-agents-concept] de GitHub Copilot son asistentes de IA especializados en tareas o ámbitos concretos del flujo de desarrollo. Se definen con archivos Markdown en `.github/agents` y pueden incluir instrucciones, prácticas recomendadas, patrones de programación y conocimiento específico. Así, los equipos pueden convertir su experiencia en agentes reutilizables: por ejemplo, un agente de accesibilidad que compruebe el cumplimiento de [WCAG][wcag], uno de seguridad o uno de pruebas.

Los agentes personalizados se definen en archivos Markdown dentro de `.github/agents` o globalmente en `~/.copilot/agents`. Cada archivo tiene un frontmatter YAML con, al menos, los campos `name` y `description`, seguido de instrucciones en Markdown.

### Agentes personalizados y habilidades de agente

Los agentes personalizados y las [habilidades de agente][agent-skills-concept] comparten algunos aspectos: ambos se describen principalmente con archivos Markdown e indican a una IA cómo realizar tareas. Una forma sencilla de distinguirlos es que el **agente personalizado** es quien trabaja y las **habilidades** son herramientas que puede utilizar.

Los agentes tienen su propia ventana de contexto y pueden coordinar habilidades e incluso otros agentes. En este taller, el agente de accesibilidad revisará y actualizará el sitio según las pautas de accesibilidad y podría usar habilidades para el flujo de PR o para ejecutar pruebas.

> [!NOTE]
> No hay una única manera correcta de crear un agente personalizado. Como con cualquier herramienta de IA, prueba distintas opciones y adáptalas a tu entorno y escenario.

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

## Escenario

Tailspin Toys quiere que su plataforma de financiación colectiva sea accesible para todas las personas. Algunos usuarios han indicado que el tema oscuro resulta difícil de leer por el bajo contraste entre texto y fondo. El equipo de diseño solicita un modo de alto contraste que se pueda activar y desactivar.

Como la accesibilidad es importante, usarás un agente personalizado para generar esta funcionalidad.

En esta lección:

- revisarás un agente personalizado de accesibilidad existente.
- asignarás una tarea al agente personalizado.

## Revisar el agente de accesibilidad

Ya hay un agente personalizado de accesibilidad. Revisa su contenido para entender cómo guiará a Copilot.

1. Vuelve a tu Codespace y abre `.github/agents/accessibility.md`.
2. Observa el frontmatter YAML con los campos `name` y `description`.

> [!CAUTION]
> El frontmatter con `name` y `description` es obligatorio para los agentes personalizados.

3. Lee las secciones siguientes, que describen sus responsabilidades, prácticas de accesibilidad, ejemplos de HTML, CSS y JavaScript, y errores habituales.

## Crear y asignar una incidencia

Mission Control es el espacio central para trabajar con todos los agentes de tu entorno. Puedes asignar tareas al agente en la nube de Copilot, supervisarlas e incluso redirigir una sesión y proporcionar indicaciones adicionales. Empecemos por asignar a Copilot la tarea de crear el modo de alto contraste.

1. Ve a tu repositorio.
2. Selecciona la pestaña **Issues**.
3. Selecciona **New issue** para abrir el cuadro de diálogo de nueva incidencia.
4. Selecciona **Blank issue** para crear la incidencia.
5. Escribe `Add high contrast mode to website` en **Title**.
6. Escribe lo siguiente en **Description**:

   ```plaintext
   We need a high contrast mode for the site. There should be a toggle for high contrast which the user can set. It should store the setting in local storage on the browser.
   ```

7. Selecciona **Create** para crear la incidencia.
8. En el panel derecho, selecciona **Assign to Copilot** para abrir el cuadro de asignación.
9. Selecciona **Accessibility agent** en la lista de agentes personalizados.

   ![Captura del cuadro de asignación del agente en la nube, con el agente personalizado y Accessibility resaltados](../../../_images/ex5-select-custom-agent.png)

10. Selecciona **Assign**.
11. Copilot empezará a trabajar en la tarea en segundo plano.

## Resumen y siguientes pasos

Esta lección ha explorado los [agentes personalizados][custom-agents] de GitHub Copilot, asistentes especializados en tareas o ámbitos concretos. Permiten convertir la experiencia y los estándares del equipo en agentes reutilizables que guían a Copilot para realizar determinados tipos de trabajo de forma más eficaz.

Has explorado estos conceptos:

- cómo se definen los agentes personalizados.
- cómo asignar una tarea a un agente personalizado.

Mientras Copilot trabaja en el modo de alto contraste, puedes pasar a [supervisar y dirigir la sesión del agente][next-lesson] desde Mission Control.

## Recursos

- [Acerca de los agentes personalizados][custom-agents]
- [Preparar la organización para usar agentes personalizados][org-custom-agents]
- [Preparar la empresa para usar agentes personalizados][enterprise-custom-agents]

[previous-lesson]: ../2-cloud-agent/
[next-lesson]: ../4-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[org-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents
[enterprise-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents
