---
slug: es-es/real-world-development/vscode
title: "Visual Studio Code"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

**[GitHub Copilot Chat](https://code.visualstudio.com/docs/copilot/chat/copilot-chat)** integra GitHub Copilot en el editor de código que ya utilizas. En Visual Studio Code y GitHub Codespaces usarás Copilot Chat en modo de agente, conectarás herramientas externas mediante MCP y trabajarás con agentes personalizados sin salir del IDE, donde Copilot puede acceder a tus archivos, al terminal y a los problemas.

Empezarás añadiendo instrucciones personalizadas y observando cómo las sigue Copilot. Después, usarás el modo de agente para crear una funcionalidad de filtrado en la interfaz, la capa de datos y las pruebas. Conectarás MCP de Playwright para que Copilot pruebe la funcionalidad en un navegador antes de abrir una solicitud de incorporación de cambios. Por último, revisarás y usarás un agente personalizado de accesibilidad y supervisarás, dirigirás e iterarás sobre los cambios desde el editor.

## Lecciones

| Lección | Tema | Descripción |
|----------|-------|-------------|
| [0. Requisitos previos][ex0] | Configuración | Crea el repositorio y un Codespace |
| [1. Instrucciones personalizadas][ex1] | Contexto | Añade y comprueba instrucciones personalizadas en VS Code |
| [2. Modo de agente][ex2] | Generación de código | Crea una funcionalidad de filtrado con el modo de agente |
| [3. MCP con Playwright][ex3] | Herramientas externas | Prueba la funcionalidad en un navegador con el servidor MCP de Playwright |
| [4. Agentes personalizados][ex4] | Agentes especializados | Revisa y usa agentes personalizados |
| [5. Supervisar agentes][ex5] | Supervisión | Supervisa y dirige las sesiones de agente |
| [6. Iterar][ex6] | Revisión | Revisa el trabajo de Copilot localmente y decide los siguientes pasos |
| [Serie opcional de Foundry Toolkit][foundry-toolkit] | Agentes de IA | Prepara un modelo, despliega un agente y conéctalo al sitio con VS Code y Foundry Toolkit |

## Requisitos previos

Antes de asistir a este taller, asegúrate de tener:

- [ ] Una cuenta de GitHub con un plan activo **Copilot Student, Pro, Pro+, Business o Enterprise**
- [ ] Acceso a GitHub Codespaces

> [!TIP]
> ¿No tienes un plan de pago? Los estudiantes verificados pueden obtener GitHub Copilot gratis mediante [GitHub Education][callout-student-plan-education]. El plan **Copilot Student** incluye las funciones de agente, MCP, revisión de código y Copilot CLI que se usan en este taller.

[callout-student-plan-education]: https://github.com/education/students

## Primeros pasos

**[Empieza por la Lección 0: Requisitos previos →][ex0]**

[ex0]: 0-prerequisites/
[ex1]: 1-custom-instructions/
[ex2]: 2-agent-mode/
[ex3]: 3-mcp/
[ex4]: 4-custom-agents/
[ex5]: 5-managing-agents/
[ex6]: 6-iterating/
[foundry-toolkit]: 7-foundry-toolkit/
