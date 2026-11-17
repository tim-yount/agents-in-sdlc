---
title: "练习 4 - 监控和管理智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

在最近几次练习中，你让 Copilot 云智能体处理了三项独立任务，用于改善用户体验和添加功能。云智能体会异步自主工作，但监控这些任务依然很重要。

有许多工具可用于管理分配给云智能体的任务，包括 GitHub.com 上的[智能体页面][agents-page]。在这个任务控制中心，你可以查看所有拥有未关闭拉取请求 (PR) 的智能体任务。你可以查看执行的操作，也可以为正在进行的会话提供指导。

本课将介绍如何：

- 探索智能体页面并监控云智能体任务。
- 引导正在进行的会话添加其他功能。

## 场景

将任务分配给智能体以创建高对比度模式后，团队意识到也可以同时添加浅色模式。由于已经在更新网站样式并添加切换功能，因此顺便加入该功能很合理。现在，你将引导智能体，同时实现浅色模式和高对比度模式。

## 查看 Copilot 云智能体任务

查看当前分配给 Copilot 云智能体的所有任务状态。

1. 访问 [Copilot 智能体页面](https://github.com/copilot/agents)。
2. 查看主窗格和左侧窗格中的任务列表。你应能看到分配给 Copilot 的任务，包括：
    - 更新代码文档。
    - 为修改游戏生成 API。
    - 为网站添加高对比度模式。
3. 选择一项正在运行的任务，查看 Copilot 已执行的操作，包括：
    - 检出存储库中的代码。
    - 创建 Copilot 的工作环境。
    - 设置 MCP 服务器。
    - 执行完成指定任务所需的其他操作。

> [!NOTE]
> 显示的具体步骤会根据 Copilot 当前的工作状态和执行方式而有所不同。

4. 同时留意右侧显示的 PR 窗格。在此处可以查看 PR 和更改的文件，以便进一步监控。

## 引导云智能体

查看任务状态后，让 Copilot 在实现高对比度模式的同时添加浅色模式切换开关。

1. 选择与添加高对比度模式相关的会话。确切标题取决于 Copilot 使用的名称和当前工作状态。

    ![任务控制中心中的无障碍会话](../../../_images/ex6-accessibility-session.png)

2. 观察会话几分钟，直到设置完成并开始执行任务。届时你会看到类似以下内容的消息。
3. 在 **Steer active session while Copilot is working** 对话框中，添加以下提示：

    ```plaintext
    While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
    ```

    ![Copilot 智能体页面中的任务截图，突出显示“Steer active session while Copilot is working”对话框](../../../_images/ex6-steer-cloud-agent-task.png)

4. 按 <kbd>Enter</kbd> 发送提示。
5. 注意 Copilot 会确认收到提示并将其纳入工作流程。

## 等待 Copilot 完成工作

Copilot 会像之前一样继续处理更新后的任务！它会在完成你发送消息时正在执行的具体步骤后，将新请求纳入工作流程。

与之前一样，这需要几分钟。此时可以暂停一下，回顾迄今为止学到和探索的内容。

## 总结和后续步骤

本课介绍了 Copilot 智能体页面，这是监控和引导 GitHub Copilot 云智能体任务的中心位置。你可以通过此任务控制中心跟踪所有正在进行和已完成的任务、审查工作过程，并调整正在执行的任务范围或提供补充指导。

你了解了以下内容：

- 探索任务控制中心和智能体页面，监控云智能体任务。
- 引导正在进行的会话添加其他功能。

Copilot 正在完成无障碍功能。接下来，[迭代 Copilot 创建的拉取请求][next-lesson]。

## 资源

- [Copilot 智能体页面][agents-page]
- [关于自定义智能体][custom-agents]

---

| [← 上一课：自定义智能体][previous-lesson] | [下一课：迭代 Copilot 的工作 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
