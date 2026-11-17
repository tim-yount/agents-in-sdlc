---
title: "Lección 1: Instrucciones personalizadas (agente en la nube)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

El contexto es fundamental cuando trabajas con IA generativa. Si una tarea debe realizarse de una forma concreta o Copilot necesita información previa, asegúrate de que tenga acceso a ella. Los [archivos de instrucciones][instruction-files] proporcionan indicaciones para que Copilot entienda no solo *qué* debe hacer, sino también *cómo*.

En esta lección:

- explorarás cómo llegan a Copilot el contexto del proyecto, las directrices de programación y los estándares de documentación mediante las instrucciones del repositorio y las instrucciones específicas para determinadas rutas.
- añadirás un estándar general a `.github/copilot-instructions.md`.

> [!NOTE]
> A diferencia de los recorridos de VS Code y CLI, aquí no compararás el resultado de un prompt antes y después: el agente en la nube trabaja de forma asíncrona con incidencias de GitHub, por lo que su efecto es más difícil de mostrar en tiempo real. Verás cómo influyen las instrucciones cuando revises las PR del agente en las lecciones siguientes.

## Archivos de instrucciones

### Escenario

Tailspin Toys tiene varias directrices de desarrollo:

- La capa de datos siempre necesita pruebas unitarias.
- La interfaz debe usar el modo oscuro y tener un aspecto moderno.
- El código debe incluir documentación en forma de comentarios TSDoc.
- Cada archivo debe empezar con un bloque de comentarios que describa su función.

Con los archivos de instrucciones, proporcionarás a Copilot la información necesaria para que realice el trabajo de acuerdo con estas prácticas.

### Instrucciones personalizadas

Las instrucciones personalizadas proporcionan contexto y preferencias a Copilot. Puedes especificar convenciones de código, bibliotecas y los comentarios que prefieres. Crea instrucciones para todo el repositorio o para tareas y tipos de archivo concretos.

Hay dos tipos de archivos:

- `.github/copilot-instructions.md` se envía a Copilot en todas las solicitudes del repositorio. Debe contener información general del proyecto, como su pila tecnológica y sus estándares.
- `.github/instructions/*.instructions.md` contiene directrices para tareas o tipos de archivo concretos, como TypeScript, Astro, componentes de interfaz o pruebas.

> [!NOTE]
> En un IDE, los archivos de instrucciones se usan para generar código con Copilot Chat, pero no para completados de código ni sugerencias de siguiente edición. Copilot Chat, Copilot CLI y el agente en la nube utilizan tanto las instrucciones del repositorio como los archivos `*.instructions.md` que tienen frontmatter `applyTo`.
>
> Copilot también admite otros formatos de instrucciones, como AGENTS.md y CLAUDE.md.

### Prácticas recomendadas para gestionar las instrucciones

- Mantén `copilot-instructions.md` centrado en la información general del proyecto y los estándares globales.
- Usa `*.instructions.md` para tipos de archivo, como pruebas unitarias, componentes Astro o la capa de datos, o para tareas concretas.
- Escribe en lenguaje natural y claro. Incluye ejemplos de cómo debería y no debería ser el código.

No existe una única manera correcta de crear archivos de instrucciones. Experimenta para encontrar el enfoque adecuado para tu proyecto.

> [!TIP]
> Todo proyecto con GitHub Copilot puede beneficiarse de una colección sólida de archivos de instrucciones. Explora las instrucciones de este proyecto para [actualizaciones de la interfaz][ui-instructions] y [Astro][astro-instructions]. Copilot también puede ayudarte a generar archivos de instrucciones, por ejemplo, con **Configure Chat → Generate Agent Instructions** en VS Code o con `/init` en Copilot CLI. Para obtener plantillas, consulta [awesome-copilot][awesome-copilot].

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## Explorar los archivos de instrucciones del proyecto

El repositorio incluye un archivo `copilot-instructions.md` y varios archivos `*.instructions.md`. Ábrelos en el editor o en la interfaz web de GitHub.

1. Abre `.github/copilot-instructions.md`.
2. Revisa secciones como **Agent notes**, **Code standards**, **Scripts** y **Repository Structure**, incluida la guía **GitHub Actions Workflows** dentro de **Code standards**.
3. Explora la carpeta `.github/instructions`, donde hay indicaciones para Astro, Drizzle, pruebas y otros ámbitos.
4. Abre `.github/instructions/unit-tests.instructions.md` y observa el campo `applyTo`. En este caso, coincide con archivos de prueba TypeScript como los que usan `**/*.test.ts`.
5. Revisa las indicaciones para crear pruebas unitarias.
6. Abre `.github/instructions/drizzle.instructions.md` y consulta sus enlaces a otros archivos de instrucciones y ejemplos del proyecto. Las rutas son relativas al propio archivo.

> [!NOTE]
> La sección **Code formatting requirements** documenta los estándares del proyecto, pero aún no exige documentación en el código. En los pasos siguientes añadirás esa directriz y los encabezados de comentarios de archivo.

## Añadir un estándar para todo el repositorio

El agente en la nube utilizará la nueva directriz al trabajar en las incidencias que le asignes.

1. En el terminal del Codespace, crea una rama:

   ```bash
   git checkout -b custom-instructions-cloud
   ```

2. Abre `.github/copilot-instructions.md` y localiza **Code formatting requirements**, cerca de la línea 27.
3. Añade estas líneas debajo de los estándares existentes:

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. Guarda `copilot-instructions.md`.

> [!TIP]
> Las instrucciones globales pertenecen a `.github/copilot-instructions.md`; las instrucciones `*.instructions.md` corresponden a lenguajes, tipos de archivo o tareas concretos.

## Confirmar, enviar y combinar el cambio

El agente en la nube lee las instrucciones de la rama de destino de la incidencia. En el siguiente ejercicio, partirá de `main`, así que debes combinar las instrucciones en esa rama.

1. Prepara y confirma el cambio:

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. Envía la rama:

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. En github.com, abre una PR desde `custom-instructions-cloud` a `main` y combínala. Así el agente podrá leer las instrucciones al trabajar en las próximas lecciones.

> [!TIP]
> Si prefieres usar `main` directamente en este taller, puedes omitir la rama y confirmar el cambio en `main`. La rama permite practicar un flujo habitual.

## Resumen y siguientes pasos

Has explorado cómo Copilot utiliza los archivos de instrucciones del proyecto y has añadido un estándar general a `.github/copilot-instructions.md`. Verás su efecto en las PR que genere el agente durante el resto del recorrido.

A continuación, [asignarás tu primera incidencia al agente en la nube][next-lesson].

## Recursos

- [Archivos de instrucciones para personalizar GitHub Copilot][instruction-files]
- [Prácticas recomendadas para crear instrucciones personalizadas][instructions-best-practices]
- [Cinco consejos para redactar mejores instrucciones personalizadas][copilot-instructions-five-tips]
- [Awesome Copilot: colección de instrucciones y otros recursos][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
