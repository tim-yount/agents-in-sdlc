---
title: "Lección 7: Crear y usar un agente de QA"
description: "Crea un agente personalizado de QA que combine los requisitos de la incidencia, la habilidad quality-checks y MCP de Playwright."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Has utilizado la habilidad `quality-checks` para ejecutar comprobaciones automatizadas y MCP de Playwright para observar el filtrado en un navegador. Ahora reunirás esas capacidades en un agente personalizado con un proceso de QA definido.

En esta lección:

- explorarás cómo un agente personalizado combina instrucciones, habilidades y herramientas MCP.
- crearás y revisarás un perfil reutilizable de control de calidad.
- seleccionarás el agente de QA y revisarás sus conclusiones respecto a la incidencia.

## Escenario

Tailspin Toys quiere revisar de forma coherente los requisitos, la calidad del código, las comprobaciones automatizadas, la cobertura de pruebas y el comportamiento en el navegador antes de abrir una PR. Un agente personalizado puede coordinar el proceso de QA y generar un informe reutilizable.

## ¿Qué es un agente personalizado?

Un agente personalizado es una versión especializada de Copilot definida en un perfil Markdown. El perfil describe su propósito, instrucciones y herramientas disponibles. En este taller definirás el rol de QA en `.github/agents/qa.agent.md` y lo seleccionarás en Copilot CLI.

Las personalizaciones que has utilizado tienen funciones distintas. Las instrucciones del repositorio describen los estándares del equipo. La habilidad `quality-checks` reúne comprobaciones repetibles. MCP de Playwright proporciona herramientas de navegador. El perfil de QA indica a Copilot cómo utilizar esas capacidades para evaluar requisitos y comunicar los resultados. No sustituye a las otras herramientas ni requiere otra conversación.

## Crear el perfil de QA

Antes de abrir la PR de la funcionalidad, pide a Copilot que cree un perfil de QA reutilizable. El perfil definirá tanto las comprobaciones como sus límites.

1. Vuelve a tu Codespace y confirma que la conversación de filtrado está en modo Interactive.
2. Pide al agente predeterminado que cree el agente personalizado:

   ```plaintext
   Create a custom agent named QA in .github/agents/qa.agent.md. It should check features against their issues and agreed requirements, follow the repository instructions, run the quality-checks skill, use Playwright MCP to verify behavior, and add tests when coverage is missing.

   Have it report each requirement as pass, fail, or blocked with supporting evidence. It must ask before changing implementation code, and it must not commit changes or open pull requests.

   Just create the profile for now so I can review it.
   ```

## Revisar el perfil

Antes de usar el agente, revisa su perfil para confirmar que Copilot captó el flujo de QA y sus límites.

1. Escribe `/diff` y abre `.github/agents/qa.agent.md`.
2. Lee el frontmatter. `description` es obligatorio; `name` es opcional, pero proporciona un nombre visible al agente.
3. Comprueba que las instrucciones empiezan por los requisitos, siguen las instrucciones del repositorio, ejecutan `quality-checks` y utilizan MCP de Playwright.
4. Confirma que el agente aporta pruebas, pide permiso antes de modificar código de implementación y no crea commits ni PR.
5. Si falta alguna responsabilidad o límite, pide al agente predeterminado que lo corrija.

## Ejecutar QA respecto a la incidencia

Copilot CLI carga los agentes del proyecto al iniciar una conversación. Reanuda la conversación de filtrado y selecciona QA para que pueda usar la incidencia y las decisiones de planificación.

1. Activa el agente con este comando:

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> Es posible que el agente no aparezca en la lista justo después de crearlo. El comando anterior lo activará.

2. Pide al agente de QA que revise la funcionalidad:

   ```plaintext
   Review the filtering feature against the issue and the decisions in our plan. Is it ready for a PR?
   ```

3. Espera a que termine el trabajo.
4. Lee el informe.

## Resumen y siguientes pasos

Has añadido un rol especializado reutilizable y has revisado su trabajo. En esta lección:

- exploraste cómo un agente personalizado combina instrucciones, habilidades y herramientas MCP.
- creaste y revisaste un perfil reutilizable de control de calidad.
- seleccionaste el agente de QA y revisaste sus conclusiones respecto a la incidencia.

Ya tienes la implementación, la actualización de la habilidad, el perfil de QA, las pruebas y el informe de verificación listos para revisar. A continuación, [reunirás todo en una PR de funcionalidad y usarás Agent Merge][next-lesson].

## Recursos

- [Crear agentes personalizados para Copilot CLI][create-agents]
- [Configuración de agentes personalizados][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
