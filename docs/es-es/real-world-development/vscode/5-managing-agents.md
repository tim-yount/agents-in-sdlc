---
title: "Lección 5: Supervisar y gestionar agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lección anterior: Agentes personalizados][previous-lesson]

En modo de agente, GitHub Copilot explora el código, propone cambios, edita archivos y ejecuta comandos. Como trabaja en tu equipo en tiempo real, Copilot Chat en VS Code muestra las llamadas a herramientas y los cambios a medida que ocurren. Puedes revisar cada diferencia, aceptar o rechazar cambios y enviar prompts de seguimiento.

En esta lección:

- supervisarás en tiempo real el trabajo del agente de accesibilidad.
- revisarás y aceptarás los cambios propuestos.
- pedirás al agente que añada un modo claro junto al alto contraste.

## Escenario

El agente personalizado de accesibilidad de la [Lección 4][previous-lesson] está implementando el modo de alto contraste. Mientras trabaja, el equipo de diseño pide añadir también un modo claro. En lugar de empezar una conversación nueva, ampliarás la tarea en la sesión actual.

## Supervisar el progreso de Copilot

Copilot Chat muestra cada paso del agente: archivos que explora, comandos que ejecuta y cambios que propone. Cada edición aparece con controles **Keep** y **Undo**.

1. Vuelve a la vista Copilot Chat de la lección anterior.
2. Mientras trabaja el agente, observa las llamadas a herramientas, lecturas, ediciones y solicitudes de comandos del terminal.
3. En cada diferencia, selecciona **Keep** para aceptar el cambio o **Undo** para revertirlo y pedir otro intento.
4. Abre el indicador **Files changed** para revisar todos los archivos modificados durante la sesión.

> [!NOTE]
> Si una llamada a una herramienta requiere permiso, por ejemplo, para ejecutar un comando del terminal, el agente mostrará **Allow**. Aprueba solo los comandos que te parezcan adecuados.

5. Espera a que termine el modo de alto contraste y revisa el resumen de los cambios.

## Pedir al agente que añada el modo claro

La conversación actual conserva el contexto de la tarea, incluidos los componentes modificados, el enfoque de estilo y el patrón de almacenamiento local.

1. Envía este prompt de seguimiento en Copilot Chat:

   ```plaintext
   Nice work! Now add a light-mode toggle alongside the high-contrast toggle. Light mode should follow the same pattern — persist via local storage and be accessible from the same area of the UI. The user should be able to enable high-contrast and light mode independently.
   ```

2. El agente revisará los cambios existentes y propondrá los cambios necesarios para el modo claro.
3. Revisa cada edición y usa **Keep** o **Undo**.
4. Si el agente sigue un enfoque que no quieres, deténlo con el botón **Stop** y envía una indicación para aclarar lo que necesitas.

> [!TIP]
> Dirigir una sesión en curso puede ser más rápido que empezar de nuevo. Usa prompts de seguimiento para pedir ajustes (por ejemplo, «simplifica el CSS; usa variables CSS en lugar de duplicar selectores»), corregir el rumbo (por ejemplo, «no añadas un tercer control; integra el modo claro en el panel de configuración existente») o ampliar el alcance (por ejemplo, «añade también atajos de teclado para ambos controles»).

## Revisar los cambios

Antes de confirmar el trabajo, revisa todos los archivos modificados.

1. Abre **Source Control** en VS Code.
2. Revisa la lista completa de archivos. Deberías ver cambios en los componentes Astro, los estilos y las pruebas relacionadas.
3. Inspecciona las diferencias y confirma el uso de atributos ARIA, navegación por teclado, HTML semántico y almacenamiento local.
4. Cuando estés conforme, prepara y confirma los cambios en el panel Source Control. Los publicarás en la lección siguiente.

## Resumen y siguientes pasos

Has supervisado y dirigido una sesión de Copilot Chat, has revisado cada cambio propuesto y has ampliado el trabajo con un modo claro.

En esta lección:

- supervisaste el trabajo del agente en tiempo real.
- aceptaste y rechazaste cambios individuales.
- ampliaste la sesión con prompts de seguimiento.

En la [siguiente lección][next-lesson] publicarás el trabajo de accesibilidad como solicitud de incorporación de cambios y revisarás los cambios del agente local.

## Recursos

- [Copilot Chat en VS Code][copilot-chat-vscode]
- [Usar el modo de agente][agent-mode]

---

| [← Lección anterior: Agentes personalizados][previous-lesson] | [Siguiente lección: Iterar sobre el trabajo de Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../4-custom-agents/
[next-lesson]: ../6-iterating/
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
