---
title: "Lección 2: Añadir funcionalidad con el modo de agente de Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Incluso los cambios más sencillos suelen requerir modificar varios archivos y ejecutar pruebas. Como desarrollador, normalmente tienes que localizar los archivos pertinentes, aplicar los cambios, ejecutar pruebas, depurar, encontrar el archivo que falta y volver a modificarlo. El modo de agente de Copilot puede coordinar este trabajo.

El modo de agente funciona de forma autónoma en el IDE. Explora la estructura del proyecto, realiza cambios en varios archivos, ejecuta tareas como las pruebas e intenta corregir los errores que encuentra. En esta lección usarás el modo de agente para añadir una funcionalidad.

> [!NOTE]
> Aunque los nombres se parecen, el modo de agente y el agente en la nube ofrecen experiencias distintas. El modo de agente trabaja en el IDE y permite ciclos de respuesta rápidos. El agente en la nube trabaja de forma asíncrona con incidencias y solicitudes de incorporación de cambios.

En esta lección aprenderás cómo Copilot explora el proyecto, identifica archivos y realiza cambios coordinados en la interfaz y la capa de datos; también revisarás los cambios y las pruebas antes de integrarlos.

## Escenario

El catálogo de juegos crece y quieres permitir que los usuarios filtren por categoría y editorial. Ya has creado una función auxiliar para las editoriales en la lección anterior. Ahora completarás la capa de datos, la interfaz y las pruebas con el modo de agente de Copilot.

## Ejecutar el sitio web Tailspin Toys

Antes de realizar cambios, explora el sitio para entender su funcionalidad actual.

El sitio web es una plataforma de financiación colectiva de juegos de mesa con una temática para desarrolladores. Es una única aplicación Astro que genera páginas HTML estáticas. Las páginas consultan directamente una base de datos SQLite local mediante Drizzle ORM. No hay una API de backend independiente ni un framework de interfaz del lado cliente. Las funciones de acceso a datos reutilizables están en `src/lib/`; la interactividad usa scripts Astro pequeños y las API DOM estándar.

### Iniciar el sitio web

1. Vuelve a tu Codespace. Deberías estar en `main` después de la lección anterior.
2. Abre un terminal con <kbd>Control</kbd>+<kbd>`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
3. Actualiza `main` y crea una rama para el filtrado:

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. Inicia el sitio:

   ```bash
   npm run dev
   ```

   Cuando el servidor de desarrollo de Astro esté listo, verás un mensaje con la URL, parecido a este:

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> Si se abre un cuadro de diálogo para el navegador en `http://localhost:4321`, ciérralo seleccionando **x**.

5. Abre el sitio manteniendo pulsada la tecla <kbd>Command</kbd> (Mac) o <kbd>Ctrl</kbd> (Windows/Linux) y seleccionando la dirección del servidor Astro en el terminal.

> [!NOTE]
> En Codespaces, al seleccionar el enlace localhost en el terminal, se redirige a una dirección como `https://<your-codespace-name>-4321.app.github.dev/`. Es un túnel privado a tu Codespace.

### Explorar el sitio

La página principal muestra una lista de juegos con títulos, imágenes y descripciones. Al seleccionar un juego, se abre una página de detalles con información como el título, la descripción, la editorial y la categoría.

## Explorar el backlog con Copilot

> [!TIP]
> **Abrir Copilot Chat**
>
> Vuelve al Codespace, abre Copilot Chat y selecciona **New Chat** para iniciar una conversación nueva. El modo y el modelo pueden variar; las instrucciones de cada ejercicio indican cuándo seleccionarlos.

La implementación inicial del sitio funciona, pero queremos ampliarla con nuevas funcionalidades. Empecemos por revisar el backlog. Al configurar el proyecto desde la plantilla se creó automáticamente un backlog de incidencias; pide a Copilot que te muestre esos elementos.

1. Selecciona **Agent** en el selector de agentes de la vista Chat.

   ![Captura del selector de agentes en la vista Chat](../../../_images/shared-chat-mode-selector.png)

2. Selecciona **Claude Sonnet 4.5** en la lista de modelos disponibles.

> [!CAUTION]
> Los autores no expresan preferencia por un modelo concreto. Se usó Claude Sonnet 4.5 al crear el taller y se incluye en estas instrucciones con la esperanza de que las sugerencias sean relativamente coherentes y la experiencia resulte satisfactoria. Sin embargo, los modelos de lenguaje son probabilísticos, por lo que las sugerencias pueden diferir de las descritas en el taller. Es normal y esperable.

> [!NOTE]
> Copilot puede usar un comando MCP diferente, pero debería completar la tarea.

3. Envía este prompt:

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

4. Selecciona **Continue** para permitir que se enumeren las incidencias.
5. Revisa la lista y la priorización.

Observa cómo Copilot ha priorizado los elementos según cuáles considera más útiles para el usuario.

## Revisar los archivos de instrucciones

Antes de pedirle al agente que genere código, revisa el archivo de instrucciones de interfaz (`.github/instructions/ui.instructions.md`), que proporciona contexto sobre cómo ampliar el sitio.

1. Abre `.github/instructions/ui.instructions.md` en el Codespace.
2. Revisa las directrices generales para ampliar el sitio, entre ellas:
   - una descripción de la arquitectura.
   - principios de diseño de componentes, pruebas y accesibilidad.
   - enlaces a archivos de instrucciones específicos para Astro, Tailwind CSS y Drizzle.

> [!TIP]
> Los archivos de instrucciones pueden enlazar otros archivos y ejemplos. Las rutas son relativas al archivo de instrucciones, lo que permite reutilizar y dividir las instrucciones en secciones pequeñas.

## Implementar el filtrado

Para completar el filtrado, la aplicación necesita varios cambios:

- añadir o ajustar la lógica restante en la capa de datos (`src/lib/`).
- añadir o actualizar las pruebas de comportamiento del filtrado.
- actualizar la página de juegos para incluir la interfaz de filtrado.

Antes de combinar los cambios, también deben ejecutarse correctamente las pruebas.

1. Continúa en la conversación actual o selecciona **New Chat**.
2. Selecciona **Add Context**, **Instructions** y **ui**.

   ![Ejemplo de cómo seleccionar el archivo de instrucciones de interfaz](../../../_images/ex3-select-instructions-file.png)

3. Confirma que está seleccionado **Agent**.

   ![Captura del selector de agentes en la vista Chat](../../../_images/shared-chat-mode-selector.png)

4. Confirma que está seleccionado **Claude Sonnet 4.5**.
5. Envía este prompt:

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

6. Observa cómo Copilot explora el proyecto, localiza la capa de datos, la interfaz y las pruebas, modifica los archivos y ejecuta las pruebas.

   ![Copilot explora los archivos del proyecto](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> Copilot realizará varias tareas: explorar el proyecto, modificar archivos y ejecutar pruebas. El proceso puede tardar unos minutos, según la complejidad de la tarea y del código. Mientras trabaja, es posible que aparezcan los botones **Keep** y **Undo** en el editor. Al terminar, habrá un botón **Keep** o **Undo** para cada cambio; no hace falta seleccionarlos mientras el agente sigue trabajando.

7. Cuando Copilot lo solicite, selecciona **Continue** para ejecutar las pruebas.

   ![Cuadro de Copilot Chat que pide confirmar si quieres ejecutar las pruebas](../../../_images/ex3-agent-mode-run-tests.png)

8. Puede haber pausas e incluso algunas pruebas pueden fallar durante el proceso. No pasa nada: Copilot alterna entre generar código y ejecutar pruebas hasta completar la tarea sin detectar errores.

   ![Sesión completada de Copilot Agent Mode](../../../_images/ex3-agent-mode-proposed-changes.png)

9. Revisa el código generado para detectar posibles problemas.

> [!CAUTION]
> Revisa siempre el código generado por Copilot o cualquier otra herramienta de IA.

10. Vuelve al navegador con el sitio en ejecución y explora la nueva funcionalidad.
11. Cuando hayas confirmado que funciona y revisado el código, selecciona **Keep** en Copilot Chat.

## Resumen y siguientes pasos

¡En este ejercicio has aprendido a usar el modo de agente de GitHub Copilot para añadir funcionalidades al sitio web de Tailspin Toys! Has visto cómo:

- el modo de agente de GitHub Copilot implementa nuevas funcionalidades en la interfaz y la capa de datos.
- el modo de agente de Copilot explora el proyecto, identifica los archivos pertinentes y coordina cambios.
- revisar los cambios y las pruebas generados por el modo de agente de Copilot antes de combinar el código en el repositorio.

A continuación, [probarás la funcionalidad con el servidor MCP de Playwright][next-lesson] y abrirás una solicitud de incorporación de cambios.

### Ejercicio adicional: implementar paginación

Cuando crezca la lista de juegos, puede que necesites implementar la paginación. Con lo aprendido en este ejercicio, pide a Copilot que actualice el sitio. Al preparar el prompt:

- sigue las prácticas recomendadas existentes, incluidos los archivos de instrucciones.
- decide cómo quieres implementar la paginación y si el usuario podrá elegir el tamaño de página o si será fijo.
- proporciona a Copilot el contexto necesario para que implemente la solución que necesitas.
- ten en cuenta que quizá debas iterar, pedir cambios y proporcionar contexto. ¡Es normal al trabajar con Copilot!

## Recursos

- [Modos ask, edit y agent de Copilot: diferencias y usos][choose-mode]
- [Modo de agente en VS Code][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
