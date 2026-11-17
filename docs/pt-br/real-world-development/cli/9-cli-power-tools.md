---
title: "Lição 9 - Comandos slash do GitHub Copilot CLI"
description: "Explore comandos slash para gerenciar o contexto, escolher modelos, compartilhar sessões e delegar tarefas à nuvem se quiser."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Como qualquer boa ferramenta de CLI, o GitHub Copilot CLI inclui vários comandos slash. Eles dão acesso a funcionalidades avançadas, informações internas e opções de configuração adicionais. Você já usou comandos como `/diff`, `/mcp`, `/skills`, `/agent` e `/pr`. Vamos explorar outros comandos úteis.

Nesta lição, você vai:

- usar `/context` e `/compact` para explorar como o Copilot gerencia o contexto da conversa.
- usar `/model` para explorar os modelos disponíveis.
- aprender como `/share` exporta ou compartilha uma sessão.
- explorar comandos opcionais para trabalho em paralelo, worktrees e delegação ao agente na nuvem.

## Cenário

Você concluiu o fluxo de trabalho principal do CLI. Agora vamos conhecer outras capacidades: gerenciar o contexto, alternar entre modelos, compartilhar sessões e, se quiser, delegar tarefas ao [agente na nuvem do Copilot][about-cloud-agent].

## Explore o contexto do Copilot CLI

Em tarefas maiores ou mais complexas, você pode atingir o limite de contexto do modelo. O Copilot CLI compacta a conversa automaticamente quando necessário, e você pode inspecionar ou compactar o contexto com comandos slash.

1. Retorne ao Codespace e inicie o Copilot CLI na raiz do repositório, se ele ainda não estiver aberto.
2. Digite:

   ```plaintext
   /context
   ```

3. Observe o modelo, o uso atual de tokens e a divisão do contexto entre instruções do sistema, ferramentas, mensagens e espaço livre.
4. Compacte a conversa:

   ```plaintext
   /compact
   ```

5. Digite `/context` novamente e compare o resultado. Talvez não haja uma grande diferença se a conversa já for curta.

> [!NOTE]
> O Copilot CLI compacta o contexto automaticamente quando a janela fica cheia. Use `/compact` para escolher o momento. Use `/clear` ou `/new` ao mudar para uma tarefa sem relação e iniciar uma conversa limpa.

## Escolha um modelo

Modelos diferentes têm capacidades diferentes, e cada desenvolvedor tem suas próprias preferências. O Copilot CLI permite listar e escolher o modelo que você quer usar.

1. Digite:

   ```plaintext
   /model
   ```

2. Explore os modelos disponíveis e as informações de uso.
3. Mantenha o modelo atual, selecione outro ou pressione <kbd>Esc</kbd> para fechar a lista.

## Compartilhe uma sessão

Trabalhar em equipe e compartilhar o que foi aprendido ajuda todos a melhorar o uso das ferramentas de IA. O comando `/share` pode exportar uma sessão para um arquivo Markdown ou HTML, criar um link compartilhável ou publicar um gist do GitHub.

1. Digite `/help` e consulte as opções de `/share` na versão instalada.
2. Se quiser compartilhar esta sessão, escolha o destino adequado, como `/share file` para exportá-la como um arquivo Markdown local.
3. Revise o conteúdo exportado antes de enviá-lo a alguém ou publicá-lo. As exportações de sessões podem incluir prompts, respostas e detalhes do projeto.

Publicar um link ou gist é opcional. Não publique conteúdo do repositório ou da conversa que a equipe não queira compartilhar.

## Opcional: amplie o trabalho ou delegue

O fluxo de trabalho principal do workshop terminou. O Copilot CLI também oferece comandos para tarefas maiores:

- `/fleet` pode dividir subtarefas independentes entre subagentes e executá-las em paralelo.
- `/worktree` pode criar uma worktree isolada do Git para outra tarefa.
- `/delegate` pode enviar uma tarefa ao agente na nuvem do Copilot, que trabalha de forma assíncrona e pode abrir uma pull request.

Esses comandos são opcionais porque podem criar worktrees adicionais ou iniciar trabalho remoto. Comece uma tarefa nova e bem delimitada antes de experimentá-los, e revise o resultado pelo fluxo de trabalho habitual. Para saber mais sobre o trabalho assíncrono com agentes, continue com o [workshop do agente na nuvem][cloud-workshop].

## Resumo e próximos passos

Os comandos slash do Copilot CLI permitem configurá-lo, compartilhar sessões e ver o que acontece nos bastidores. Nesta lição, você:

- usou `/context` e `/compact` para explorar como o Copilot gerencia o contexto da conversa.
- usou `/model` para explorar os modelos disponíveis.
- aprendeu como `/share` exporta ou compartilha uma sessão.
- explorou comandos opcionais para trabalho em paralelo, worktrees e delegação ao agente na nuvem.

Há muitos outros comandos slash para explorar. Vamos encerrar nossa jornada [revisando o que aprendemos][next-lesson] e conhecendo os próximos passos.

## Recursos

- [Referência de comandos do Copilot CLI][cli-reference]
- [Gerenciamento de contexto no Copilot CLI][context-management]
- [Sobre o agente na nuvem do Copilot][about-cloud-agent]

[previous-lesson]: ../8-create-pull-request/
[next-lesson]: ../10-review/
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[context-management]: https://docs.github.com/copilot/concepts/agents/copilot-cli/context-management
[about-cloud-agent]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-workshop]: ../../cloud/
