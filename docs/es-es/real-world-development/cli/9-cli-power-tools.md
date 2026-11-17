---
title: "Lección 9: Comandos de barra de GitHub Copilot CLI"
description: "Explora comandos de barra para gestionar el contexto, seleccionar modelos, compartir sesiones y delegar tareas opcionalmente en la nube."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Como cualquier herramienta de CLI, GitHub Copilot CLI incluye muchos comandos de barra. Estos permiten acceder a funciones avanzadas, información interna y opciones de configuración. Ya has usado comandos como `/diff`, `/mcp`, `/skills`, `/agent` y `/pr`. Ahora explorarás otros útiles.

En esta lección:

- usarás `/context` y `/compact` para explorar cómo gestiona Copilot el contexto de la conversación.
- usarás `/model` para ver los modelos disponibles.
- aprenderás cómo `/share` puede exportar o compartir una sesión.
- explorarás comandos opcionales para trabajar en paralelo, usar worktrees y delegar trabajo al agente en la nube.

## Escenario

Ya has completado el flujo principal de CLI. Ahora explorarás funciones adicionales: administrar el contexto, cambiar de modelo, compartir sesiones y delegar tareas opcionalmente en [Copilot cloud agent][about-cloud-agent].

## Explorar el contexto de Copilot CLI

En tareas grandes o complejas puedes acercarte al límite de contexto del modelo. Copilot CLI compacta automáticamente la conversación cuando es necesario, y puedes inspeccionar o compactar el contexto con comandos de barra.

1. Vuelve a tu Codespace e inicia Copilot CLI desde la raíz del repositorio si todavía no está abierto.
2. Escribe:

   ```plaintext
   /context
   ```

3. Consulta el modelo, el uso actual de tokens y la distribución del contexto entre instrucciones del sistema, herramientas, mensajes y espacio libre.
4. Compacta la conversación:

   ```plaintext
   /compact
   ```

5. Vuelve a escribir `/context` y compara el resultado. Si la conversación es pequeña, puede que el cambio no sea grande.

> [!NOTE]
> Copilot CLI compacta automáticamente el contexto cuando se llena la ventana. Usa `/compact` para decidir cuándo hacerlo. Usa `/clear` o `/new` para iniciar una conversación nueva al cambiar a una tarea distinta.

## Elegir un modelo

Los modelos tienen distintas capacidades y cada desarrollador puede tener sus preferencias. Copilot CLI permite consultar y seleccionar el modelo.

1. Escribe:

   ```plaintext
   /model
   ```

2. Explora los modelos disponibles y su información de uso.
3. Mantén el modelo actual, selecciona otro o pulsa <kbd>Esc</kbd> para cerrar la lista.

## Compartir una sesión

Compartir el trabajo y los aprendizajes ayuda al equipo. El comando `/share` puede exportar una sesión a un archivo Markdown o HTML, crear un enlace para compartir o publicar un gist de GitHub.

1. Escribe `/help` y consulta las opciones de `/share` disponibles en tu versión.
2. Si quieres compartir la sesión, elige el destino adecuado; por ejemplo, `/share file` para exportar un archivo Markdown local.
3. Revisa el contenido exportado antes de enviarlo o publicarlo. Las exportaciones pueden incluir prompts, respuestas y detalles del proyecto.

Publicar un enlace o un gist es opcional. No publiques contenido del repositorio o de una conversación que el equipo no quiera compartir.

## Opcional: ampliar o delegar el trabajo

El flujo principal del taller ha terminado. Copilot CLI también tiene comandos para tareas mayores:

- `/fleet` puede dividir tareas independientes entre subagentes y ejecutarlas en paralelo.
- `/worktree` puede crear un worktree de Git aislado para una tarea distinta.
- `/delegate` puede enviar una tarea a Copilot cloud agent, que trabaja de forma asíncrona y puede abrir una PR.

Estos comandos son opcionales: pueden crear worktrees adicionales o iniciar trabajo remoto. Empieza con una tarea nueva y acotada, y revisa el resultado con tu flujo habitual. Para profundizar en el trabajo asíncrono con agentes, continúa con el [taller de agentes en la nube][cloud-workshop].

## Resumen y siguientes pasos

Los comandos de barra de Copilot CLI permiten configurarlo, compartir sesiones y consultar qué ocurre en segundo plano. En esta lección:

- usaste `/context` y `/compact` para explorar cómo gestiona Copilot el contexto.
- usaste `/model` para explorar los modelos disponibles.
- aprendiste cómo `/share` puede exportar o compartir sesiones.
- exploraste comandos opcionales para trabajar en paralelo, usar worktrees y delegar tareas.

Copilot CLI incluye muchos más comandos de barra. Para cerrar el recorrido, [repasarás lo aprendido][next-lesson] y descubrirás los pasos siguientes.

## Recursos

- [Referencia de comandos de Copilot CLI][cli-reference]
- [Gestión del contexto en Copilot CLI][context-management]
- [Acerca de Copilot cloud agent][about-cloud-agent]

[previous-lesson]: ../8-create-pull-request/
[next-lesson]: ../10-review/
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[context-management]: https://docs.github.com/copilot/concepts/agents/copilot-cli/context-management
[about-cloud-agent]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-workshop]: ../../cloud/
