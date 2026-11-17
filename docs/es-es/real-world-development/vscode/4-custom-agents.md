---
title: "Lección 4: Agentes personalizados"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## ¿Qué son los agentes personalizados?

Los [agentes personalizados][custom-agents-concept] de GitHub Copilot permiten crear asistentes de IA especializados y adaptados a tareas o ámbitos concretos del flujo de desarrollo. Al definirlos mediante archivos Markdown en la carpeta `.github/agents` del repositorio, puedes proporcionar a Copilot instrucciones específicas, prácticas recomendadas, patrones de programación y conocimientos del dominio que le ayuden a realizar determinados tipos de trabajo con mayor eficacia. Los equipos pueden convertir su experiencia en agentes reutilizables: por ejemplo, uno de accesibilidad que haga cumplir [WCAG][wcag], uno de seguridad que siga prácticas de programación segura o uno de pruebas que mantenga patrones de pruebas coherentes.

Los agentes se definen en archivos Markdown dentro de `.github/agents` o globalmente en `~/.copilot/agents`. Cada archivo tiene un frontmatter YAML con, al menos, `name` y `description`, seguido de las instrucciones del agente.

### Agentes personalizados y habilidades de agente

Los agentes personalizados y las [habilidades de agente][agent-skills-concept] comparten algunos aspectos: ambos indican a una IA cómo realizar tareas. Una forma sencilla de distinguirlos es que el **agente personalizado** es quien trabaja y las **habilidades** son herramientas que puede utilizar.

Los agentes personalizados tienen su propia ventana de contexto y están diseñados para coordinar habilidades e incluso otros agentes como parte de su trabajo. En este taller, el agente personalizado de accesibilidad revisará y actualizará el sitio según las pautas de accesibilidad; para hacerlo, podría utilizar habilidades como la de flujo de trabajo de solicitudes de incorporación de cambios o una que ejecute y gestione pruebas.

> [!NOTE]
> No hay una única manera correcta de crear un agente personalizado. Prueba e itera para encontrar lo que funciona en tu entorno.

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

## Escenario

Tailspin Toys quiere que su plataforma sea accesible para todas las personas. Algunos usuarios han indicado que el tema oscuro resulta difícil de leer por el bajo contraste. El equipo de diseño solicita un modo de alto contraste que se pueda activar y desactivar.

En esta lección:

- revisarás el agente personalizado de accesibilidad existente.
- usarás ese agente en Copilot Chat para implementar un modo de alto contraste.

Como la accesibilidad es fundamental, queremos implementar esta función cuanto antes. Para ello, usarás un agente personalizado que genere la funcionalidad.

## Revisar el agente de accesibilidad

Ya hay un agente personalizado de accesibilidad. Revisa su contenido para entender cómo guiará a Copilot.

1. Vuelve a tu Codespace y abre un terminal.
2. Crea una rama nueva desde `main` para mantener separada la PR de filtrado:

   ```bash
   git checkout main
   git pull
   git checkout -b accessibility-vscode
   ```

3. Abre `.github/agents/accessibility.md`.
4. Comprueba el frontmatter YAML, que incluye los campos `name` y `description`.

> [!CAUTION]
> El frontmatter con `name` y `description` es obligatorio para los agentes personalizados.

5. Revisa las responsabilidades, las prácticas de accesibilidad, los ejemplos de HTML, CSS y JavaScript, y los errores habituales.

## Usar el agente personalizado en Copilot Chat

VS Code muestra los agentes personalizados de `.github/agents` en el selector de agentes situado en la parte inferior de Copilot Chat. Puedes seleccionar un agente para aplicar sus instrucciones y herramientas a la conversación.

> [!TIP]
> **Abrir Copilot Chat**
>
> Antes de empezar los ejercicios siguientes, vuelve al Codespace, abre Copilot Chat y selecciona **New Chat** para iniciar una conversación nueva. El modo y el modelo pueden variar según el ejercicio; las instrucciones indicarán cuándo seleccionarlos.

1. Selecciona **Agent** en el selector de agentes de la vista Chat, si aún no está seleccionado.

   ![Captura del selector de agentes en la vista Chat](../../../_images/shared-chat-mode-selector.png)

2. Selecciona el menú desplegable de agentes situado en la parte inferior de la vista Chat (muestra el agente activo; de forma predeterminada es **default**).
3. Selecciona **Accessibility agent** en la lista de agentes disponibles.
4. Envía el siguiente prompt al agente de accesibilidad:

   ```plaintext
   Add a high-contrast mode to the site. There should be a toggle for high contrast which the user can set, and the setting should persist across page reloads using local storage on the browser.
   ```

5. Copilot Chat explorará el código base, propondrá cambios y los aplicará a los archivos del proyecto. Cada edición aparecerá en línea en el chat, con la ruta del archivo y una diferencia que podrás revisar.
6. A medida que se apliquen los cambios, el indicador **Files changed** mostrará el conjunto de archivos que el agente ha modificado.

> [!NOTE]
> Copilot puede tardar varios minutos. Modificará archivos reales del proyecto, como componentes Astro, CSS y pruebas.

En la lección siguiente revisarás y dirigirás el trabajo que el agente está realizando.

## Resumen y siguientes pasos

Esta lección ha explorado los [agentes personalizados][custom-agents] de GitHub Copilot, asistentes de IA especializados en tareas o ámbitos concretos. Permiten convertir la experiencia y los estándares del equipo en agentes reutilizables que guían a Copilot para realizar determinados tipos de trabajo con mayor eficacia.

Has explorado estos conceptos:

- cómo se definen los agentes personalizados.
- cómo se usa un agente personalizado en el modo de agente de Copilot Chat.

A continuación, [supervisarás y dirigirás el trabajo del agente][next-lesson], revisarás los cambios y añadirás un modo claro a la misma sesión.

## Recursos

- [Acerca de los agentes personalizados][custom-agents]
- [Crear agentes personalizados en el IDE][creating-custom-agents-ide]
- [Agentes personalizados en VS Code][custom-agents-vscode]
- [Configuración de agentes personalizados][custom-agents-config]
- [Agentes personalizados de awesome-copilot][awesome-copilot-agents]

---

| [← Lección anterior: Probar la funcionalidad con MCP de Playwright][previous-lesson] | [Siguiente lección: Supervisar y gestionar agentes →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-mcp/
[next-lesson]: ../5-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[creating-custom-agents-ide]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/create-custom-agents-in-your-ide
[custom-agents-vscode]: https://code.visualstudio.com/docs/copilot/customization/custom-agents
[custom-agents-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
[awesome-copilot-agents]: https://github.com/github/awesome-copilot/tree/main/agents
