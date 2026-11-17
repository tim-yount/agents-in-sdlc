---
title: "练习 1 - 自定义指令（云智能体）"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 上一课：先决条件][previous-lesson] · [下一课：Copilot 云智能体 →][next-lesson]

使用生成式 AI 时，上下文至关重要。如果任务需要以特定方式完成，或 Copilot 需要了解一些背景信息，就要确保它能访问这些上下文。[指令文件][instruction-files]可提供此类指导，让 Copilot 不仅了解你希望它做什么，也了解你希望它如何完成。

本练习将介绍如何：

- 通过存储库自定义指令和按路径限定的指令文件，让 Copilot 获得项目专属上下文、编码指南和文档标准。
- 向 `.github/copilot-instructions.md` 添加新的存储库级标准。

> [!NOTE]
> 与 VS Code 和 CLI 环境不同，这里不会运行更新前后对比提示。Copilot 云智能体会异步处理 GitHub 议题，因此难以实时并排展示指令的影响。后续练习中，你可以通过审查云智能体创建的拉取请求，了解指令文件的影响。

## 指令文件

### 场景

Tailspin Toys 与其他优秀的软件开发团队一样，制定了一套开发实践指南和要求，包括：

- 数据层始终需要单元测试。
- UI 应使用深色模式并具有现代感。
- 应通过 TSDoc 文档注释为代码添加文档。
- 每个文件顶部都应有一段注释，说明文件的用途。

通过使用指令文件，你可以确保 Copilot 了解这些实践要求，并据此完成任务。

### 自定义指令

自定义指令可为 Copilot 提供上下文和偏好，帮助它理解你的编码风格和要求。它可以引导 Copilot 提供更符合需求的建议和代码片段。你可以为整个存储库指定首选编码规范、库以及注释风格，也可以为特定文件类型创建任务级上下文。

指令文件有两种：

- `.github/copilot-instructions.md`：每次针对该存储库的请求都会发送给 Copilot 的单个指令文件。内容应是适用于大多数聊天或 CLI 请求的项目级指导，例如技术栈、项目概述、最佳实践和全局要求。
- `.github/instructions/*.instructions.md`：为特定语言（如 TypeScript 或 Astro）、任务（如创建 UI 组件或单元测试）提供指导的文件。

> [!NOTE]
> 在 IDE 中，指令文件只用于 Copilot Chat 代码生成，不用于代码补全或下一个编辑建议。
>
> Copilot Chat、Copilot CLI 和 Copilot 云智能体在生成代码时会使用存储库级指令和带有 `applyTo` frontmatter 的 `*.instructions.md` 文件。
>
> 此外，Copilot [还支持其他标准的指令文件][custom-instructions-support]，包括 AGENTS.md 和 CLAUDE.md。

### 管理指令文件的最佳实践

全面介绍如何创建指令文件超出了本研讨会的范围，但示例项目展示了一种有代表性的方法。总体而言：

- 将 `copilot-instructions.md` 的内容限定为项目级指导，例如项目简介、结构和全局编码标准。
- 使用 `*.instructions.md` 文件为特定文件类型（单元测试、Astro 组件、数据层）或任务提供指导。
- 使用自然语言，确保指导清晰，并提供代码示例说明应如何编写。

创建指令文件没有唯一的方法，使用 AI 也是如此。通过实践，你会找到适合项目的方法。

> [!TIP]
> 每个使用 GitHub Copilot 的项目都应具备完善的指令文件集合。探索本项目中的文件时，你可能会发现有些文件专门用于[更新 UI][ui-instructions]和 [Astro][astro-instructions] 等任务。
>
> Copilot 也可以帮你生成指令文件。不同界面的操作各不相同（例如，VS Code 中的 **Configure Chat → Generate Agent Instructions**，或 Copilot CLI 中的 `/init`）；相关课程会在适用时介绍具体方法。
>
> 想查找模板或起步示例？可以浏览 [awesome-copilot][awesome-copilot]，其中收集了指令文件、自定义智能体和其他资源。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## 探索项目中的自定义指令文件

花些时间阅读此存储库附带的指令文件：一个核心 `copilot-instructions.md` 文件，以及一组适用于不同任务的 `*.instructions.md` 文件。可在编辑器或 GitHub 网页界面中打开它们。

1. 打开 `.github/copilot-instructions.md`。
2. 浏览文件，留意项目简介以及 **Agent notes**、**Code standards**、**Scripts** 和 **Repository Structure** 等部分。**Code standards** 下还有 **GitHub Actions Workflows** 子部分。这些要求适用于你与 Copilot 的所有交互。
3. 打开 `.github/instructions` 文件夹并查看其中的文件。这里有 Astro 文件、Drizzle 数据层、测试等方面的指令。
4. 打开 `.github/instructions/unit-tests.instructions.md`。留意顶部的 `applyTo` 字段；它定义了相对于存储库根目录的 glob，用于匹配适用文件。任何符合 `**/*.test.ts` 的 TypeScript 测试文件都会匹配。
5. 留意此项目中创建单元测试的专门指令。
6. 最后，打开 `.github/instructions/drizzle.instructions.md` 并滚动到末尾。留意它对其他指令文件（如 `unit-tests.instructions.md`）和项目现有文件的链接。这样可以将较大的指令集拆分成较小、可复用的文件，并提供生成代码时可供 Copilot 参考的示例。（其中的路径相对于指令文件，而不是存储库根目录。）

> [!NOTE]
> `copilot-instructions.md` 中的 **Code formatting requirements** 部分介绍了项目编码标准，但尚未要求添加代码文档。接下来，你将添加 TSDoc 文档注释和文件级注释头的规则。

## 添加新的存储库标准

接下来，你将进行本练习唯一的一处编辑：添加一条项目级规则，要求代码文档采用 TSDoc 文档注释和文件级注释头。云智能体在本系列后续练习中处理分配给它的议题时，会遵循此规则。

编辑前，先创建分支（云智能体会读取议题目标分支中的指令，但仍建议单独提交更改）：

1. 在 Codespace 终端中创建并切换到新分支：

   ```bash
   git checkout -b custom-instructions-cloud
   ```

如前所述，`.github/copilot-instructions.md` 用于向 Copilot 提供项目级信息。现在添加一项编码标准，改善代码建议。

1. 重新打开 `.github/copilot-instructions.md`。
2. 找到 **Code formatting requirements** 部分，应该在第 27 行附近。注意该部分记录了项目编码规范，但尚未规定代码文档要求，这就是生成的辅助函数没有文档注释的原因。
3. 在现有标准下方添加以下 Markdown 内容，要求 Copilot 添加文件注释头和 TSDoc 文档注释：

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. 保存 `copilot-instructions.md`。

> [!TIP]
> 如上一课所示，可以在存储库级文件 (`.github/copilot-instructions.md`) 中设置全局指导，也可以在 `*.instructions.md` 文件中设置特定语言、文件类型或任务的指导。对于刚添加的文档注释规则等项目级标准，存储库级文件是合适的位置。

## 提交、推送并合并指令更新

云智能体会读取议题目标分支中的指令。下一练习中将议题分配给 Copilot 时，它会从 `main` 创建分支，因此必须将指令更改合并到 `main`，云智能体才能使用。

1. 暂存并提交：

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. 推送分支：

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. 在 github.com 上创建从 `custom-instructions-cloud` 合并到 `main` 的拉取请求并将其合并。这样，云智能体在后续练习中处理分配给它的议题时就会读取这些指令。

> [!TIP]
> 如果希望直接在 `main` 上完成本研讨会，也可以跳过分支步骤，直接提交到 `main`。这里保留分支步骤，是为了模拟真实项目中的处理方式。

## 总结和后续步骤

你已了解 Copilot 如何读取本项目的指令文件，并向 `.github/copilot-instructions.md` 添加了新的存储库级标准。后续练习中，你会看到云智能体创建的拉取请求如何遵循该标准。

接下来，[将第一个议题分配给 Copilot 云智能体][next-lesson]。

## 资源

- [GitHub Copilot 自定义指令文件][instruction-files]
- [创建自定义指令的最佳实践][instructions-best-practices]
- [编写更好的 Copilot 自定义指令的 5 个技巧][copilot-instructions-five-tips]
- [Awesome Copilot：指令文件及其他资源集合][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
