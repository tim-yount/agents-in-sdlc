---
title: "Lección 6: Validar la funcionalidad con MCP de Playwright"
description: "Inspecciona o configura MCP de Playwright en Copilot CLI y úsalo para explorar en el navegador la funcionalidad de filtrado."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Como ya hemos comentado, programar no consiste solo en escribir código. También hay que trabajar con datos y servicios externos, y ampliar las automatizaciones que Copilot puede utilizar. Para ello sirven los servidores MCP: permiten que Copilot CLI acceda a herramientas y servicios adicionales.

En esta lección:

- entenderás qué es Model Context Protocol (MCP) y cómo lo usa Copilot CLI.
- añadirás el servidor MCP de Playwright si todavía no está disponible.
- pedirás al agente que controle un navegador para explorar la funcionalidad de filtrado.

## Escenario

Las pruebas unitarias y de extremo a extremo son importantes, pero para validar cambios en la interfaz hace falta interactuar con ella. Quieres que Copilot use el sitio web como lo haría una persona y automatice más comprobaciones.

## ¿Qué es Model Context Protocol (MCP)?

[Model Context Protocol (MCP)][mcp-blog-post] permite que los agentes de IA se comuniquen con herramientas y servicios externos en tiempo real. Así pueden acceder a información actualizada y realizar acciones en tu nombre.

Los agentes acceden a estas herramientas y recursos a través de un servidor MCP, que actúa como puente. Cada servidor ofrece un conjunto diferente de herramientas y recursos.

Algunos servidores MCP conocidos son:

- **[GitHub MCP Server][github-mcp]**: ofrece acceso a API para gestionar repositorios, incidencias y solicitudes de incorporación de cambios de GitHub.
- **[Playwright MCP Server][playwright-mcp-server]**: ofrece automatización de navegadores con Playwright.

Hay muchos otros servidores MCP disponibles. GitHub aloja un [registro de MCP][mcp-registry] para facilitar su descubrimiento y las contribuciones al ecosistema.

> [!CAUTION]
> Trata los servidores MCP como cualquier otra dependencia del proyecto. Antes de usar uno, revisa su código fuente, comprueba quién lo publica y considera las implicaciones de seguridad.

## Añadir el servidor MCP de Playwright

Si todavía no está disponible, añade el servidor MCP de Playwright para que Copilot pueda interactuar con el sitio como lo haría una persona.

> [!NOTE]
> Si MCP de Playwright ya está configurado en Copilot CLI, omite estos pasos y continúa con la sección siguiente.

1. Vuelve a tu Codespace.
2. Abre el cuadro de diálogo para añadir un servidor MCP con este comando en Copilot CLI:

   ```plaintext
   /mcp add
   ```

3. Escribe `playwright` como nombre y pulsa <kbd>Tab</kbd>.
4. Confirma el tipo **STDIO** con <kbd>Enter</kbd> y pulsa <kbd>Tab</kbd>.
5. Pega lo siguiente en el cuadro **Command**:

   ```plaintext
   npx -y @playwright/mcp@latest --headless --no-sandbox
   ```

6. Pulsa <kbd>Control</kbd>+<kbd>S</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>S</kbd> (Windows/Linux) para guardar el servidor.
7. Pulsa <kbd>Esc</kbd> para salir del cuadro de MCP.

## Pedir a Copilot que explore la funcionalidad con Playwright

Ya has comprobado manualmente que la funcionalidad funciona. Ahora pide a Copilot que haga lo mismo con el servidor MCP de Playwright.

1. Usa este prompt para pedirle que valide la funcionalidad:

   ```plaintext
   Start the app and use Playwright MCP to check filtering against the issue and our plan. Tell me what works and what doesn't, without making changes. Stop the server you started when you're done.
   ```

> [!NOTE]
> No es imprescindible indicar a Copilot que use MCP: normalmente lo detectará. Aun así, mencionar la herramienta ayuda a obtener resultados más coherentes.

2. Observa los pasos que ejecuta Copilot en el navegador.
3. Lee el informe y confirma que todo se comporta como esperas.

Copilot iniciará el servidor, usará Playwright para interactuar con el sitio, detendrá el servidor y te entregará un informe.

## Resumen y siguientes pasos

Has usado el servidor MCP de Playwright para explorar la funcionalidad en un navegador real desde Copilot CLI. En esta lección:

- aprendiste qué es Model Context Protocol (MCP) y cómo lo usa Copilot CLI.
- añadiste el servidor MCP de Playwright si no estaba disponible.
- pediste al agente que controlara un navegador para explorar la funcionalidad de filtrado.

A continuación, [crearás un agente personalizado de QA][next-lesson] que combinará la habilidad y las herramientas del navegador.

## Recursos

- [¿Qué es MCP y por qué habla todo el mundo de ello?][mcp-blog-post]
- [Servidor MCP de Microsoft Playwright][playwright-mcp-server]
- [Añadir servidores MCP a Copilot CLI][add-mcp]

[previous-lesson]: ../5-agent-skills/
[next-lesson]: ../7-qa-agent/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[add-mcp]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers
