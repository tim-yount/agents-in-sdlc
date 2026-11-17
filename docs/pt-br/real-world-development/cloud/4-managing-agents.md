---
title: "Exercício 4 - Monitoramento e gerenciamento de agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Nos últimos exercícios, você pediu ao agente na nuvem do Copilot que executasse três tarefas para aprimorar a experiência de usuário e adicionar funcionalidades. Embora o agente na nuvem trabalhe de forma autônoma e assíncrona, ainda é importante monitorar essas tarefas.

Você pode gerenciar tarefas atribuídas ao agente na nuvem com várias ferramentas, incluindo a [página de agentes][agents-page] no GitHub.com. Nesse Mission Control, você vê todas as tarefas dos agentes com pull requests (PRs) abertas. É possível explorar as operações realizadas e orientar uma sessão em andamento.

Nesta lição, você vai:

- explorar a página de agentes para monitorar tarefas do agente na nuvem.
- orientar uma sessão em andamento e solicitar uma funcionalidade adicional.

## Cenário

Depois de atribuir ao agente a criação de um modo de alto contraste, a equipe percebeu que seria útil adicionar também um modo claro. Como o trabalho já atualizaria o estilo do site e incluiria um controle de alternância, pareceu lógico adicionar essa funcionalidade. Você orientará o agente para garantir que ele implemente também o modo claro.

## Revise as tarefas do agente na nuvem do Copilot

Vamos verificar o status atual das tarefas atribuídas ao agente na nuvem do Copilot.

1. Acesse a [página de agentes do Copilot](https://github.com/copilot/agents).
2. Observe a lista de tarefas no painel principal e no painel esquerdo. Ela deve mostrar as tarefas atribuídas ao Copilot, incluindo:
    - atualizar a documentação do código.
    - gerar APIs para modificar jogos.
    - adicionar um modo de alto contraste ao site.
3. Selecione uma tarefa em execução. Revise as etapas executadas pelo Copilot, que podem incluir:
    - clonar o código do repositório.
    - criar o ambiente de trabalho do Copilot.
    - configurar servidores MCP.
    - realizar várias ações para concluir a tarefa.

> [!NOTE]
> As etapas listadas variam de acordo com o estado do trabalho e a abordagem usada.

4. Observe também o painel de pull request (PR) à direita. Ele permite acompanhar a PR e os arquivos alterados.

## Oriente o agente na nuvem

Agora que você viu as tarefas em andamento, vamos pedir ao Copilot que inclua o modo claro enquanto trabalha no modo de alto contraste.

1. Selecione a sessão sobre a criação de um modo de alto contraste. O título exato depende do nome escolhido pelo Copilot e do estado do trabalho.

    ![Sessão de acessibilidade no Mission Control](../../../_images/ex6-accessibility-session.png)

2. Acompanhe a sessão por alguns minutos, até que ela indique que a configuração terminou e o trabalho começou. Você verá mensagens semelhantes aos exemplos abaixo.
3. Na caixa de diálogo **Steer active session while Copilot is working**, adicione o seguinte prompt:

    ```plaintext
    While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
    ```

    ![Tarefa do agente na nuvem com a caixa de diálogo para orientar a sessão ativa destacada](../../../_images/ex6-steer-cloud-agent-task.png)

4. Pressione <kbd>Enter</kbd> para enviar o prompt.
5. Observe como o Copilot confirma o recebimento do prompt e o inclui no fluxo de trabalho.

## Deixe o Copilot trabalhar

Como antes, o Copilot trabalhará na tarefa atualizada. Ele incorporará a nova solicitação ao fluxo depois de concluir a etapa em andamento quando você enviou a mensagem.

Como o processo pode levar alguns minutos, aproveite para fazer uma pausa e refletir sobre o que aprendeu até aqui.

## Resumo e próximos passos

Esta lição apresentou a página de agentes do Copilot, o centro de monitoramento e orientação das tarefas do agente na nuvem do GitHub Copilot. Nela, você acompanha tarefas ativas e concluídas, revisa o trabalho e redireciona sessões em andamento.

Você explorou estes conceitos:

- usar o Mission Control e a página de agentes para monitorar tarefas do agente na nuvem.
- redirecionar uma sessão em andamento e solicitar funcionalidades adicionais.

Enquanto o Copilot conclui o trabalho nos recursos de acessibilidade, vamos [iterar nas pull requests criadas pelo Copilot][next-lesson].

## Recursos

- [Página de agentes do Copilot][agents-page]
- [Sobre agentes personalizados][custom-agents]

---

| [← Lição anterior: Agentes personalizados][previous-lesson] | [Próxima lição: Iterar no trabalho do Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
