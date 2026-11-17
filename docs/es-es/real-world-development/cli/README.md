---
slug: es-es/real-world-development/cli
title: "GitHub Copilot CLI"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

**[GitHub Copilot CLI](https://docs.github.com/copilot/concepts/agents/about-copilot-cli)** integra GitHub Copilot en tu terminal como asistente de programación con agentes. Explora bases de código, genera código, ejecuta comandos y se conecta a herramientas externas desde la línea de comandos.

En este taller instalarás y autenticarás Copilot CLI, y después iniciarás un flujo de desarrollo con Tailspin Toys. Añadirás valoraciones por estrellas, trabajarás desde una incidencia con los modos Plan y Autopilot, actualizarás instrucciones y habilidades, y validarás la funcionalidad con MCP de Playwright. A continuación, crearás un agente de QA, usarás Agent Merge para gestionar una solicitud de incorporación de cambios y explorarás comandos de barra y delegación opcional al agente en la nube.

## Lecciones

| Lección | Tema | Descripción |
|----------|-------|-------------|
| [0. Requisitos previos][ex0] | Configuración | Crea una copia del proyecto Tailspin Toys y prepara un Codespace |
| [1. Instalar GitHub Copilot CLI][ex1] | Instalación | Instala y autentica Copilot CLI, y encuentra la incidencia de filtrado |
| [2. Añadir valoraciones por estrellas][ex2] | Primer cambio | Muestra las valoraciones de los juegos y combina tu primera PR |
| [3. Modos de agente: Plan y Autopilot][ex3] | Modos de agente | Planifica la funcionalidad desde una incidencia y desarróllala con Autopilot |
| [4. Guiar a Copilot con instrucciones personalizadas][ex4] | Contexto | Explora y actualiza las instrucciones del repositorio |
| [5. Personalizar y usar una habilidad quality-checks][ex5] | Comprobaciones | Personaliza una habilidad y ejecútala para comprobar el proyecto |
| [6. Validar la funcionalidad con MCP de Playwright][ex6] | Herramientas externas | Usa Playwright para explorar la funcionalidad en un navegador |
| [7. Crear y usar un agente de QA][ex7] | Agentes | Revisa requisitos, cobertura y pruebas con un agente especializado |
| [8. Crear y combinar la PR de la funcionalidad][ex8] | Revisión | Revisa el cambio y deja que Agent Merge gestione la PR |
| [9. Comandos de barra][ex9] | Funciones de CLI | Explora el contexto, los modelos, el uso compartido y la delegación |
| [10. Repaso y siguientes pasos][ex10] | Resumen | Repasa el flujo de trabajo y los recursos adicionales |
| [Serie opcional de Foundry][foundry] | Agentes hospedados | Prepara un modelo, crea y despliega un agente y conéctalo al sitio |

## Requisitos previos

Antes de asistir a este taller, asegúrate de tener:

- [ ] Una cuenta de GitHub con un plan activo **Copilot Student, Pro, Pro+, Business o Enterprise**
- [ ] Conocimientos básicos de las operaciones de terminal y línea de comandos
- [ ] Git instalado y configurado

> [!TIP]
> ¿No tienes un plan de pago? Los estudiantes verificados pueden obtener GitHub Copilot gratis mediante [GitHub Education][callout-student-plan-education]. El plan **Copilot Student** incluye las funciones de agente, MCP, revisión de código y Copilot CLI que utiliza este taller.

[callout-student-plan-education]: https://github.com/education/students

> [!NOTE]
> Si utilizas Copilot Business o Copilot Enterprise, asegúrate de que el administrador haya habilitado Copilot CLI.

## Primeros pasos

**[Empieza por la Lección 0: Requisitos previos →][ex0]**

[ex0]: 0-prerequisites/
[ex1]: 1-install-copilot-cli/
[ex2]: 2-add-star-rating/
[ex3]: 3-agent-modes/
[ex4]: 4-custom-instructions/
[ex5]: 5-agent-skills/
[ex6]: 6-mcp-playwright/
[ex7]: 7-qa-agent/
[ex8]: 8-create-pull-request/
[ex9]: 9-cli-power-tools/
[ex10]: 10-review/
[foundry]: 8-foundry-agent/
