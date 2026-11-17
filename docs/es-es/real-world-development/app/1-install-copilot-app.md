---
title: "Lección 1: Instalar la aplicación GitHub Copilot"
description: "Instala la aplicación GitHub Copilot, conecta el repositorio creado a partir de la plantilla, conoce el espacio de trabajo y prueba un chat rápido."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

La **[aplicación GitHub Copilot][about-copilot-app]** es una aplicación de escritorio para el desarrollo dirigido por agentes. Se basa en GitHub Copilot CLI y se integra de forma nativa con GitHub, por lo que los repositorios, las ramas y las canalizaciones de CI funcionan sin configuración adicional. Está diseñada para flujos de trabajo en los que diriges varios agentes en paralelo, cada uno en su propio espacio de trabajo aislado, en lugar de realizar todo el trabajo por tu cuenta, y automatizas tareas repetitivas. Con Node.js instalado y la copia del proyecto preparada, el siguiente paso es instalar la aplicación y conectar el repositorio.

En esta lección:

- instalarás la aplicación GitHub Copilot e iniciarás sesión.
- añadirás el proyecto a la aplicación desde su repositorio de GitHub.
- conocerás el espacio de trabajo y el backlog que creó la plantilla.
- probarás un chat rápido para conocer la propia aplicación.

## Escenario

Tu equipo está adoptando agentes de IA para abordar una lista creciente de trabajo pendiente. La aplicación Copilot ofrece un único lugar desde el que dirigir ese trabajo: seleccionar incidencias, ejecutar agentes, revisar cambios y combinar solicitudes de incorporación de cambios. En esta lección instalarás y conectarás la aplicación y aprenderás a iniciar una conversación sobre el proyecto.

> [!NOTE]
> Se requiere un plan de Copilot apto: Copilot Free, Copilot Student o cualquier plan de pago (Pro, Pro+, Business o Enterprise). Si utilizas Copilot Business o Copilot Enterprise, el administrador debe mantener habilitada la directiva **GitHub Copilot app**.

## Instalar y configurar la aplicación GitHub Copilot

La aplicación tiene versiones para Windows, macOS y Linux. Instálala, autentícate y añade el repositorio Tailspin Toys.

1. En un navegador, abre la [página de la aplicación GitHub Copilot][download-app].
2. Descarga la aplicación para tu plataforma e instálala siguiendo las instrucciones de la página.
3. Abre la aplicación.
4. Selecciona **Sign in to GitHub** y sigue las instrucciones para iniciar sesión con una cuenta de GitHub.com o GHE.com. Si usas GitHub Enterprise Cloud con residencia de datos, selecciona **GitHub Enterprise Cloud** e introduce el nombre de host `*.ghe.com` cuando se te solicite.

   Si usas GitHub Enterprise Server, completa primero la incorporación con tu cuenta en la nube. Después, abre **Settings**, selecciona **Accounts**, selecciona **Add account** y elige **GitHub Enterprise Server**. Sigue las instrucciones para autorizar la aplicación en el navegador; consulta la [guía de inicio de sesión de Enterprise Server][ghes-sign-in].

5. Si el proceso de incorporación te permite seleccionar un repositorio, selecciona Tailspin Toys, creado a partir de la plantilla. También puedes omitir este paso y añadir el proyecto más adelante.
6. Elige un tema cuando se te solicite y termina la incorporación.
7. Busca el repositorio en **Sessions**, en la barra lateral. Si ya aparece, no hace falta volver a añadirlo.
8. Si todavía no está conectado, selecciona **+** junto a **Sessions** para crear una sesión y, después, selecciona **Add GitHub repository**. Usa el propietario y el nombre de repositorio que anotaste en la lección de requisitos previos.
9. Confirma que el repositorio aparece en la barra lateral. En esta disposición, las carpetas de repositorio, como `tailspin-toys`, aparecen agrupadas en **Sessions**, y las sesiones individuales están debajo de cada repositorio.

## Conocer el espacio de trabajo

La barra lateral organiza el trabajo en estas áreas:

- **New**: inicia una nueva sesión de chat con Copilot.
- **Pull requests**: explora y filtra solicitudes de incorporación de cambios, consulta el estado de CI y revísalas mediante la integración nativa con GitHub.
- **Issues**: explora y filtra incidencias e inicia una sesión a partir de una incidencia.
- **Automations**: guarda tareas de agente para ejecutarlas según una programación o bajo demanda. Pueden gestionar listas de tareas y tareas periódicas; el repaso las presenta como siguiente paso, no como un ejercicio adicional.
- **Customize**: añade funciones a la aplicación mediante servidores MCP, plugins, habilidades y otros componentes. La usarás para configurar MCP de Playwright.
- **Chats**: ofrece conversaciones breves para preguntas y lluvias de ideas que no necesitan una rama ni un espacio de trabajo propios. Esta sección aparece después del primer chat. Si no la ves, selecciona **+** junto a **Sessions** para iniciar un chat.
- **Sessions**: agrupa las carpetas de repositorio y las sesiones de agente. Selecciona un repositorio, como `tailspin-toys`, para abrir su vista, o una sesión para volver a la conversación. Cada sesión se ejecuta en su propio espacio de trabajo aislado, por lo que puedes ejecutar varias sin que sus cambios entren en conflicto. Iniciarás la primera sesión al añadir valoraciones por estrellas.

> [!TIP]
> Si tienes dudas, pregunta a Copilot. Puede ayudarte a averiguar cómo hacer algo o si es posible.

### Encontrar el backlog inicial

Tailspin Toys ya tiene incidencias creadas cuando generaste el repositorio a partir de la plantilla.

1. En la barra lateral, selecciona la carpeta del repositorio Tailspin Toys que aparece en **Sessions**, no una sesión individual. Después, selecciona **Issues** en la navegación superior del repositorio.
2. Busca estas incidencias por su título; no des por hecho sus números:

   - Allow users to filter games by category and publisher
   - Update our repository coding standards

3. Selecciona una incidencia y lee sus detalles. Cada incidencia también permite iniciar una sesión de agente. Empezarás por la incidencia de filtrado después de realizar un primer cambio rápido.

> [!NOTE]
> Las listas de **Issues** y **Pull requests** muestran automáticamente solo elementos de los repositorios añadidos a la aplicación Copilot. Para ver elementos de otros repositorios, añádelos a la aplicación.

## Probar un chat rápido

Los chats rápidos permiten hacer una pregunta o proponer ideas sin crear una rama ni un worktree. Son adecuados para consultas breves que no requieren una sesión.

1. Selecciona **+** junto a **Chats** en la barra lateral para abrir un chat. Si todavía no ves **Chats**, selecciona **+** junto a **Sessions** para iniciar un chat; después aparecerá la sección.
2. Pregunta cómo funcionan las sesiones de la aplicación:

   ```plaintext
   How does the GitHub Copilot app use worktrees?
   ```

3. Lee la respuesta. Cada sesión se ejecuta en su propio worktree de Git aislado, lo que permite ejecutar varios agentes en paralelo sin que sus cambios entren en conflicto. Puedes continuar la conversación o iniciar otra.

## Resumen y siguientes pasos

Has instalado la aplicación GitHub Copilot, conectado el proyecto y explorado el espacio de trabajo. Has aprendido a:

- instalar la aplicación e iniciar sesión en GitHub.
- añadir un proyecto desde su repositorio de GitHub.
- conocer el espacio de trabajo y encontrar el backlog en **Issues**.
- usar un chat rápido para hacer una pregunta breve.

A continuación, [iniciarás tu primera sesión de agente][next-lesson] para mostrar valoraciones por estrellas en las tarjetas de juegos.

## Recursos

- [Acerca de la aplicación GitHub Copilot][about-copilot-app]
- [Introducción a la aplicación GitHub Copilot][getting-started]
- [Trabajar con sesiones de agente en la aplicación GitHub Copilot][agent-sessions]

[next-lesson]: ../2-add-star-rating/
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
[getting-started]: https://docs.github.com/copilot/how-tos/github-copilot-app/getting-started
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
[download-app]: https://gh.io/app
[ghes-sign-in]: https://docs.github.com/enterprise-server@3.22/copilot/copilot-on-ghes/sign-in-on-copilot-app
