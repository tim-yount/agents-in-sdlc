---
title: "Exercício 2 - Agente na nuvem do GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lição anterior: Instruções personalizadas][previous-lesson] |
|:--|

É provável que poucas organizações não enfrentem problemas de débito técnico. Pode ser necessário resolver problemas de segurança, atualizar código legado ou implementar solicitações de funcionalidades que ficaram no backlog por falta de tempo. O agente na nuvem do GitHub Copilot foi criado para tarefas como atualizar código e adicionar funcionalidades de maneira autônoma. Quando termina, ele gera uma PR de rascunho para revisão por um desenvolvedor. Isso permite delegar tarefas repetitivas, acelerar o desenvolvimento e deixar os desenvolvedores livres para se concentrar em questões mais abrangentes.

Neste exercício, você explorará como o agente na nuvem do Copilot permite:

- personalizar o ambiente de geração de código.
- garantir que as operações sejam realizadas com segurança.
- entender a importância de issues bem delimitadas.
- atribuir issues ao Copilot.

## Cenários

A Tailspin Toys tem débito técnico para resolver. Os prestadores de serviço contratados inicialmente para criar o site deixaram a documentação em um estado inadequado — na verdade, ela está totalmente ausente. Como primeiro passo, a empresa quer que comentários TSDoc sejam adicionados a todas as funções exportadas do aplicativo.

Além disso, a equipe de design quer aprimorar a descoberta de jogos. Ela gostaria que a página de detalhes de cada jogo mostrasse outros títulos da mesma categoria, permitindo que as pessoas continuem explorando. Não é necessário que a implementação esteja refinada; basta algo que permita testar a experiência de usuário. Essa tarefa está bloqueada, mas há outras issues de prioridade maior no momento.

Esses são exemplos de tarefas que podem ser adiadas e que são ideais para delegar ao agente na nuvem do Copilot. Ele pode trabalhar nelas de forma assíncrona enquanto você se concentra em outras tarefas. Depois, você revisa o trabalho e confirma que está tudo como esperado.

## Conheça o agente na nuvem do GitHub Copilot

O [agente na nuvem do GitHub Copilot](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent) executa tarefas em segundo plano, de maneira parecida com um desenvolvedor. Assim como você faria com um colega de equipe, há várias maneiras de iniciar o trabalho, incluindo [atribuir uma issue do GitHub ao Copilot](https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions). Depois da atribuição, o Copilot cria uma pull request de rascunho para acompanhar o progresso, configura um ambiente e começa a trabalhar. Você pode inspecionar a sessão enquanto o trabalho está em andamento ou depois que ele termina. Quando a solução proposta estiver pronta para revisão, o Copilot mencionará você na pull request.

## A importância de instruções bem delimitadas

O GitHub Copilot não é mágico: não é possível deixar de pensar no problema. Mesmo operações aparentemente simples ficam complexas quando examinadas de perto; por isso, [defina com cuidado o escopo das tarefas para o agente na nuvem do Copilot][cloud-agent-best-practices]. Trate-o como um parceiro de programação com IA: trabalhe por etapas, aprenda, experimente e adapte o processo. A chegada da IA generativa não altera os fundamentos do desenvolvimento de software.

## Instruções personalizadas neste repositório

Nos exercícios anteriores, você conheceu as instruções personalizadas e como elas orientam o Copilot. Se já fez o exercício prático sobre instruções personalizadas, viu `.github/copilot-instructions.md` em ação; caso contrário, este é um bom momento para dar uma olhada. Antes de atribuir trabalho ao agente na nuvem do Copilot, leia os arquivos de instruções deste repositório sem alterá-los para poder observar o impacto mais adiante.

Abra os arquivos a seguir na interface Web do GitHub ou em um Codespace, se já houver um aberto:

- `.github/copilot-instructions.md` — revise a seção **Code standards**, principalmente as expectativas sobre convenções TypeScript e comentários TSDoc.
- `.github/instructions/unit-tests.instructions.md` — observe o frontmatter `applyTo`, que aplica as instruções a arquivos `**/*.test.ts`.

Ao atribuir a issue `Code lacks documentation` ao agente na nuvem na próxima seção, observe na pull request resultante os comentários TSDoc, as convenções TypeScript e os cabeçalhos de comentários. Essas orientações vêm dos arquivos de instruções que você está examinando. Voltaremos a esse tema ao revisar as PRs em um exercício posterior.

## Configure o ambiente de desenvolvimento do agente na nuvem do Copilot

A criação de código normalmente exige um ambiente específico e alguns scripts de configuração para garantir que tudo esteja pronto. O mesmo vale ao atribuir tarefas ao Copilot, que trabalha de maneira parecida com um engenheiro de software.

O agente na nuvem usa o [GitHub Actions][github-actions] como ambiente de trabalho. Você pode personalizar esse ambiente com um [fluxo de trabalho especial de configuração][setup-workflow], definido em `.github/workflows/copilot-setup-steps.yml`, que será executado antes de o agente começar. Assim, ele terá acesso às ferramentas e dependências de desenvolvimento necessárias. Esse fluxo já está configurado para facilitar o laboratório e a experiência de aprendizagem. Ele disponibiliza Node.js, dependências do projeto, binários do navegador para testes de ponta a ponta e o banco de dados SQLite migrado e preenchido para o aplicativo Astro único:

```yaml
name: "Copilot Setup Steps"

# Permite testar as etapas de configuração na guia "Actions" do repositório
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # Defina as permissões mínimas necessárias para *suas etapas*. O Copilot receberá um token próprio para as operações dele.
    permissions:
      # Para clonar o repositório como parte da configuração, por exemplo, para instalar dependências, você precisará da permissão `contents: read`. Se não clonar o repositório nas etapas de configuração, o Copilot fará isso automaticamente depois que elas forem concluídas.
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # Configuração do front-end/aplicativo: Node.js (o aplicativo agora usa Astro + Drizzle/libSQL)
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # Migre e preencha o banco de dados SQLite local para que builds e testes tenham dados.
      - name: Set up the database
        run: npm run db:setup
```

O arquivo se parece com qualquer outro fluxo de trabalho do GitHub, mas contém alguns detalhes importantes:

- Ele contém um único trabalho chamado `copilot-setup-steps`, executado no GitHub Actions antes de o Copilot começar a trabalhar na pull request.
- O gatilho `workflow_dispatch` permite executar o fluxo manualmente na guia **Actions** do repositório. Isso é útil para testar se ele funciona, sem esperar o Copilot iniciá-lo.

## Adicione documentação

Todos entendem a importância da documentação, mas muitos projetos têm informações desatualizadas ou nenhuma documentação. Esse tipo de débito técnico costuma ficar sem solução, o que reduz a produtividade e dificulta a manutenção do código ou a integração de novos desenvolvedores. O Copilot pode ajudar a criar documentação, e esta é uma issue ideal para atribuir ao agente na nuvem. Ele trabalhará em segundo plano para produzir a documentação necessária. Em um exercício futuro, você voltará para revisar o trabalho.

1. Abra uma nova guia do navegador e acesse seu repositório no github.com.
2. Selecione a guia **Issues**.
3. Selecione **New issue** para abrir a caixa de diálogo de nova issue.
4. Selecione **Blank issue** para criar uma issue em branco.
5. Defina **Title** como `Code lacks documentation`.
6. Defina **Description** como:

    ```plaintext
    Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
    ```

7. Selecione **Create** para criar a issue.
8. No lado direito, selecione **Assign to Copilot** para abrir a caixa de diálogo de atribuição.

  ![Atribuição de uma issue ao Copilot](../../../_images/shared-assign-copilot.png)

9. Selecione **Assign**.
10. Selecione a guia **Pull Requests**.
11. Abra a nova pull request (PR), que terá um título semelhante a `[WIP]: Code lacks documentation`. Se ela ainda não aparecer na lista, aguarde alguns minutos e atualize a página.
12. Depois de alguns minutos, o Copilot deverá criar uma lista de tarefas.

> [!NOTE]
> A lista de tarefas do Copilot pode demorar alguns minutos para aparecer na PR. O Copilot está preparando o ambiente (executando o fluxo de trabalho mencionado acima), analisando o projeto e definindo uma abordagem.

13. Revise a lista e as tarefas que o Copilot pretende executar.
14. Role a linha do tempo da pull request; você deverá ver uma atualização informando que o Copilot começou a trabalhar na issue.
15. Selecione o botão **View session**.

  ![Visualização da sessão do Copilot](../../../_images/ex4-view-session.png)

> [!CAUTION]
> Talvez seja necessário atualizar a janela para ver o indicador atualizado.

16. Observe que você pode percorrer a sessão ao vivo e acompanhar a resolução do problema pelo Copilot: ele explora o código e entende o estado do projeto, pausa para pensar e decidir uma abordagem e, então, cria o código.

Isso pode levar alguns minutos. Um dos principais objetivos do agente na nuvem do Copilot é executar tarefas de forma assíncrona, deixando você livre para trabalhar em outras atividades. Vamos aproveitar esse recurso atribuindo outra tarefa ao agente e, em seguida, voltando nossa atenção à criação de funcionalidades para o aplicativo.

## Adicione uma seção de jogos relacionados à página de detalhes

Como já vimos, uma das grandes vantagens do agente na nuvem do GitHub Copilot é permitir dividir o trabalho. Você pode se concentrar em um conjunto de tarefas enquanto ele cuida de outro. Mesmo que a seção de jogos relacionados não leve muito tempo para a equipe de design, delegá-la deixa você livre para outras atividades. Vamos atribuí-la ao agente na nuvem do Copilot.

1. Retorne ao repositório no github.com.
2. Selecione a guia **Issues**.
3. Selecione **New issue** para abrir a caixa de diálogo de nova issue.
4. Selecione **Blank issue** para usar o modelo em branco.
5. Defina **Title** como `Show related games on the game details page`.
6. Defina **Description** como:

    ```markdown
    We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
   ```

7. Selecione **Create** para criar a issue.
8. No lado direito, selecione **Assign to Copilot** para abrir a caixa de diálogo de atribuição.

  ![Atribuição de uma issue ao Copilot](../../../_images/shared-assign-copilot.png)

9. Selecione **Assign**.

Pouco depois, você deverá ver 👀 no primeiro comentário da issue, indicando que o Copilot está trabalhando nela.

![O Copilot usa o emoji de olhos para indicar que está trabalhando na issue](../../../_images/ex4-issue-eyes-emoji.png)

O Copilot já está trabalhando na segunda solicitação. Como o agente na nuvem trabalha de maneira parecida com um engenheiro de software, não é necessário acompanhá-lo ativamente: basta revisar o resultado depois que ele terminar. Agora vamos criar e usar agentes personalizados.

## Resumo e próximos passos

Esta lição apresentou o [agente na nuvem do GitHub Copilot][copilot-agents]. Com ele, você pode atribuir issues ao Copilot para execução assíncrona. Você pode delegar a ele a resolução de débito técnico, a criação de funcionalidades ou a migração de código entre frameworks.

Você explorou estes conceitos:

- personalizar o ambiente de geração de código.
- garantir que as operações sejam realizadas com segurança.
- entender a importância de issues bem delimitadas.
- atribuir issues ao Copilot.

Enquanto o agente na nuvem trabalha, vamos criar e usar agentes personalizados. O [agente na nuvem do Copilot também pode usar servidores MCP][cloud-agent-mcp] e tem acesso a instruções personalizadas, que já exploramos em módulos anteriores.

## Recursos

- [Sobre o agente na nuvem do Copilot][copilot-agents]
- [Atribuir issues do GitHub ao Copilot][assign-issue]
- [Práticas recomendadas para o fluxo de configuração do agente na nuvem do Copilot][cloud-agent-best-practices]

| [Próxima lição: Agentes personalizados →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
