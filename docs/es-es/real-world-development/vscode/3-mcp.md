---
title: "Lección 3: Probar la funcionalidad con el servidor MCP de Playwright"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lección anterior: Modo de agente][previous-lesson] · [Siguiente lección: Agentes personalizados →][next-lesson]

Acabas de crear el filtrado con el modo de agente. Antes de abrir una solicitud de incorporación de cambios, comprueba que funciona en el navegador. Conectarás el **servidor MCP de Playwright** para que Copilot controle un navegador real y pruebe la funcionalidad. Después, publicarás la rama y abrirás la PR.

En esta lección:

- aprenderás qué es Model Context Protocol (MCP) y cómo los servidores MCP amplían Copilot.
- añadirás el servidor MCP de Playwright al espacio de trabajo.
- pedirás a Copilot que lo use para probar el filtrado en un navegador.
- publicarás la rama y abrirás una solicitud de incorporación de cambios.

## ¿Qué es Model Context Protocol (MCP)?

El modo de agente es más potente cuando puede acceder a recursos externos. Model Context Protocol (MCP) permite que Copilot se comunique con herramientas y servicios externos.

![Diagrama del funcionamiento del modo de agente y su interacción con el contexto, el LLM y las herramientas, incluidas las herramientas aportadas por servidores MCP y extensiones de VS Code](../../../_images/ex1-mcp-diagram.png)

[Model Context Protocol (MCP)](https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/) permite a los agentes de IA comunicarse con herramientas y servicios externos en tiempo real. Así pueden acceder a información actualizada mediante recursos y realizar acciones en tu nombre mediante herramientas.

El servidor MCP actúa como puente entre el agente y las herramientas externas, como API existentes o paquetes npm locales. Cada servidor ofrece un conjunto distinto de herramientas y recursos.

Algunos servidores MCP conocidos son:

- **[GitHub MCP Server](https://github.com/github/github-mcp-server)**: proporciona API para gestionar repositorios de GitHub, crear repositorios y administrar incidencias y solicitudes de incorporación de cambios.
- **[Playwright MCP Server](https://github.com/microsoft/playwright-mcp)**: proporciona automatización del navegador con Playwright para navegar por páginas, rellenar formularios y seleccionar botones.

GitHub aloja un [registro de MCP](https://github.com/mcp) que facilita descubrir servidores y contribuir al ecosistema.

> [!CAUTION]
> Trata los servidores MCP como cualquier otra dependencia. Antes de usar uno, revisa su código fuente, comprueba quién lo publica y considera las implicaciones de seguridad. Usa solo servidores de confianza y ten cuidado al conceder acceso a recursos u operaciones sensibles.

## Revisar la configuración de MCP

El archivo `.vscode/mcp.json` configura los servidores MCP disponibles en este espacio de trabajo.

1. Abre `.vscode/mcp.json` en tu Codespace.
2. Deberías ver un servidor `github` configurado:

   ```json
   {
     "servers": {
       "github": {
         "type": "http",
         "url": "https://api.githubcopilot.com/mcp/"
       }
     }
   }
   ```

La plantilla incluye esta entrada y por eso Copilot pudo leer el backlog en el ejercicio anterior. Usa el [servidor MCP remoto de GitHub][remote-github-mcp-server]; VS Code se conecta por HTTP y solicita la autenticación de GitHub la primera vez que se usa una herramienta.

## Añadir el servidor MCP de Playwright

El [servidor MCP de Playwright][playwright-mcp-server] proporciona a Copilot un navegador controlable.

1. Añade una entrada `playwright` junto a `github` en `.vscode/mcp.json`:

   ```json
   {
     "servers": {
       "github": {
         "type": "http",
         "url": "https://api.githubcopilot.com/mcp/"
       },
       "playwright": {
         "command": "npx",
         "args": ["@playwright/mcp@latest", "--headless"]
       }
     }
   }
   ```

2. Guarda el archivo.

El servidor `playwright` es local: VS Code lo inicia ejecutando `npx @playwright/mcp@latest`. La opción `--headless` ejecuta el navegador sin una ventana visible, necesaria en Codespaces porque no hay escritorio.

> [!NOTE]
> Tailspin Toys ya utiliza Playwright para las pruebas de extremo a extremo, así que el navegador suele estar instalado. Si Copilot indica que falta, pídele que ejecute `npx playwright install chromium`.

## Iniciar y confiar en el servidor

VS Code inicia los servidores MCP cuando se necesitan. La primera vez que Copilot necesita las herramientas, VS Code inicia el servidor y te pide que confirmes si confías en él.

1. En `.vscode/mcp.json`, selecciona **Start** sobre la entrada `playwright` para iniciar el servidor y comprobar la configuración.
2. Si VS Code te pide confirmar que confías en el servidor, revisa la configuración y selecciona la opción para confiar en él.

Este paso es opcional: si no lo inicias ahora, VS Code lo iniciará la primera vez que Copilot use las herramientas.

## Probar la funcionalidad de filtrado

El servidor MCP de Playwright permite a Copilot controlar un navegador real. En lugar de que compruebes el trabajo haciendo clic en la aplicación, el agente puede abrir una página, navegar por ella, aplicar filtros y leer los resultados para resumirte lo que ha observado. Así puedes confirmar rápidamente que la funcionalidad se comporta como esperas, sin salir de la conversación.

Por debajo, el servidor MCP de Playwright utiliza el [árbol de accesibilidad][playwright-mcp-server] de la página en lugar de capturas de pantalla. El agente razona sobre elementos estructurados y etiquetados (botones, enlaces y elementos de lista), igual que las tecnologías de asistencia. Por eso una comprobación funcional rápida también sirve como una revisión básica de accesibilidad.

Con el servidor conectado y la aplicación en ejecución, pide a Copilot que pruebe la funcionalidad:

```text
Using the Playwright MCP server, open a browser to the running app at http://localhost:4321 and verify the new game filtering feature:

1. Go to the games page and note how many games are listed.
2. Apply a category filter and confirm the list updates to only show games in that category.
3. Clear it, then apply a publisher filter and confirm the list updates to that publisher.
4. Combine a category and a publisher filter and confirm the results respect both.

Report what you observe at each step, and call out anything that does not behave as expected.
```

Copilot abrirá un navegador mediante el servidor MCP de Playwright, seguirá los pasos y te comunicará lo que haya encontrado. Compara el informe con los criterios de aceptación de la incidencia. Si algo no funciona, haz preguntas de seguimiento o pide que corrija el código antes de abrir la PR.

> [!NOTE]
> La aplicación debe estar disponible en `http://localhost:4321`. Si has detenido el servidor de desarrollo, vuelve a iniciarlo. La primera vez, Playwright puede necesitar descargar un navegador; si falta, ejecuta `npx playwright install chromium`.

## Publicar la rama y crear una solicitud de incorporación de cambios

1. Abre el panel **Source Control** de Codespaces y revisa los cambios de Copilot.
2. Selecciona el icono **+** para preparar los cambios.
3. Usa el botón **Sparkle** para generar un mensaje de confirmación.

   ![Panel Source Control con los cambios realizados](../../../_images/ex3-source-control-changes.png)

4. Selecciona **Publish** para enviar la rama al repositorio.

## Crear la solicitud de incorporación de cambios

Copilot puede localizar la incidencia y crear una PR asociada.

1. Abre Copilot Chat y selecciona **New Chat**.
2. Selecciona **Agent** en el selector de agentes.
3. Pide a Copilot que cree una PR:

   ```plaintext
   Find the issue in the repo related to filtering by category and publisher. Create a new pull request for the current branch, and associate it with the correct issue.
   ```

4. Selecciona **Continue** cuando sea necesario para permitir que Copilot obtenga información y realice las operaciones. La primera vez que use una herramienta de GitHub puede pedirte que te autentiques.
5. Revisa cómo encuentra la incidencia correcta y crea la PR.
6. Selecciona el enlace de Copilot para revisar la PR, pero **no la combines todavía**.

## Resumen y siguientes pasos

Has aprendido qué es MCP, añadido Playwright y usado el servidor para probar la funcionalidad en un navegador antes de publicarla. También has enviado la rama y abierto una PR.

A continuación, [crearás un agente personalizado][next-lesson] para agilizar tareas concretas, como las revisiones de accesibilidad.

## Recursos

- [¿Qué es MCP y por qué habla todo el mundo de ello?][mcp-blog-post]
- [Servidor MCP de Microsoft Playwright][playwright-mcp-server]
- [Servidor MCP de GitHub][github-mcp-server]
- [Registro de GitHub MCP][mcp-registry]
- [Servidores MCP en VS Code][vscode-mcp-config]

[previous-lesson]: ../2-agent-mode/
[next-lesson]: ../4-custom-agents/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp-server]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[remote-github-mcp-server]: https://github.blog/changelog/2025-06-12-remote-github-mcp-server-is-now-available-in-public-preview/
[vscode-mcp-config]: https://code.visualstudio.com/docs/agents/reference/mcp-configuration
