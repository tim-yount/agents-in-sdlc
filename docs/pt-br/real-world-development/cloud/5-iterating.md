---
title: "Exercício 5: Iterando no trabalho do GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lição anterior: Gerenciar agentes][previous-lesson] |
|:--|

## Revise o trabalho

Durante este laboratório, você trabalhou com o GitHub Copilot em várias tarefas para aprimorar a experiência de usuário e adicionar funcionalidades. Você pediu ao Copilot que documentasse o código, criasse uma funcionalidade de jogos relacionados para a equipe de design iterar e implementasse recursos de acessibilidade, incluindo controles para os modos de alto contraste e claro. Vamos explorar as alterações e, se necessário, orientar o Copilot para melhorar o resultado.

### Cenário

Como já destacamos várias vezes, os fundamentos do design de software e do DevOps não mudam com a chegada da IA generativa. Sempre precisamos revisar o código gerado e seguir o processo normal de DevOps. Vamos revisar as sugestões do GitHub Copilot para a documentação, os jogos relacionados e os recursos de acessibilidade antes de habilitar a revisão pela equipe.

## Segurança e o agente na nuvem do GitHub Copilot

Como o agente na nuvem do Copilot executa tarefas de forma assíncrona e sem supervisão, existem restrições de segurança para manter o ambiente protegido. Entre elas:

- O Copilot tem acesso de leitura ao repositório e acesso de gravação **somente** ao branch que usará para o código.
- O agente na nuvem é executado no GitHub Actions, em um ambiente separado e temporário.
- Os fluxos de trabalho do GitHub Actions precisam de aprovação humana antes de serem executados.
- [O acesso a recursos externos é limitado por padrão](https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall), incluindo o acesso a servidores MCP.

## Revise a documentação gerada

Vamos começar pela primeira pull request (PR) criada pelo agente na nuvem do GitHub Copilot: a que adiciona documentação ao código. Você fará essa revisão usando a interface padrão de PRs do GitHub.com.

> [!NOTE]
> Ao abrir a PR, talvez você veja um aviso de que o GitHub Copilot foi bloqueado por um firewall. Isso é **esperado**, pois o Copilot tem acesso limitado a recursos externos por padrão, incluindo servidores MCP externos. Se quiser, você pode [personalizar ou desabilitar o firewall do agente na nuvem do Copilot][agent-firewall].

1. Retorne ao seu repositório no github.com.
2. Selecione **Pull Requests** para abrir a lista de pull requests.
3. Abra a PR com um título semelhante a **Add missing documentation**.

> [!NOTE]
> Se o Copilot ainda estiver trabalhando na tarefa, a PR terá o marcador **[WIP]**. Nesse caso, aguarde o término do trabalho. Isso pode levar alguns minutos; aproveite para fazer uma pausa ou refletir sobre o que aprendeu.

4. Quando a PR estiver pronta, selecione a guia **Files changed** e revise as alterações.

    ![Guia Files changed](../../../_images/shared-pr-files-changed.png)

5. Explore o código atualizado, que inclui os comentários TSDoc e outras documentações. As alterações exatas variam.

    Procure comentários TSDoc, convenções TypeScript e cabeçalhos de comentários. Eles foram definidos nos arquivos de instruções personalizadas que você examinou no início do Exercício 2.

6. Depois de revisar as atualizações, retorne à guia **Conversation** e role a página para baixo.
7. Você deverá ver um indicador de que alguns fluxos de trabalho aguardam aprovação.
8. Se houver fluxos aguardando aprovação, selecione **Approve and run workflows**.

   ![Aprovar e executar fluxos de trabalho](../../../_images/shared-approve-workflows.png)

9. Os fluxos deverão entrar na fila da seção de verificações da pull request. Se tudo correr bem, as verificações do projeto para o aplicativo Astro único serão aprovadas. Isso pode levar alguns minutos.

## Peça alterações ao GitHub Copilot

Trabalhar com o Copilot em uma pull request não é uma via de mão única. Você pode mencionar o Copilot em comentários da PR, como faria com outra pessoa da equipe, ou em comentários de linha no código. O Copilot verá esses comentários e iniciará outra sessão para atendê-los. Como os resultados são não determinísticos, não podemos indicar um texto específico para solicitar. Algumas ideias:

- Adicionar cabeçalhos de comentário no início de cada arquivo de código, com uma descrição breve da finalidade.
- Adicionar comentários TSDoc a arquivos TypeScript e Astro.
- Criar um README com uma descrição da estrutura do aplicativo Astro.

1. Adicione um comentário solicitando uma alteração na documentação gerada e mencione **@copilot**, como faria com qualquer pessoa. Use uma das ideias acima ou outra sugestão sobre a documentação do código.
2. Selecione **View Session** para acompanhar o Copilot. Observe que ele inicia uma nova sessão para fazer as atualizações.
3. Selecione **Back to pull request** para retornar à PR.

    ![Retornar à pull request](../../../_images/ex7-back-to-pr.png)

4. Quando o Copilot concluir as alterações, deverá aparecer um novo commit na pull request.
5. Selecione a guia **Files changed** para revisar as alterações.

Continue iterando até ficar satisfeito. Depois, você pode converter a PR de rascunho em pronta para revisão e mesclá-la ao branch principal.

![Converter PR em pronta para revisão](../../../_images/ex7-ready-for-review.png)

## Revise a funcionalidade de jogos relacionados

Agora, vamos voltar à PR criada pelo Copilot para resolver a issue de jogos relacionados na página de detalhes de cada jogo.

1. Retorne ao repositório no GitHub.com.
2. Selecione a guia **Pull Requests**.
3. Selecione a PR com um título semelhante a **Show related games on the game details page**.
4. Selecione a guia **Files changed** para revisar o código criado.
5. Depois de revisar as atualizações, retorne à guia **Conversation** e role a página para baixo.
6. Você deverá ver um indicador de que alguns fluxos de trabalho aguardam aprovação.
7. Se houver fluxos aguardando aprovação, selecione **Approve and run workflows**.

   ![Aprovar e executar fluxos de trabalho](../../../_images/shared-approve-workflows.png)

8. Os fluxos deverão entrar na fila da seção de verificações da pull request. Se tudo correr bem, as verificações do projeto para o aplicativo Astro único serão aprovadas. Isso pode levar alguns minutos.
9. **Opcional:** você pode alternar para esse branch no Codespace para testar manualmente a funcionalidade de jogos relacionados. Acesse o Codespace, abra o terminal e execute estes comandos (substitua `<branch-name>` pelo nome do branch criado pelo Copilot, por exemplo, **copilot/fix-8**):

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

O Copilot criou a funcionalidade de jogos relacionados. Assim como antes, você pode iterar com o agente na nuvem e solicitar atualizações. Por exemplo, peça ao Copilot para alterar a quantidade de jogos relacionados ou adicionar cabeçalhos de comentários e comentários TSDoc (lembre-se: a issue foi atribuída **antes** de você atualizar as instruções). Para isso, adicione um comentário na guia **Conversation**; o Copilot verá a solicitação e iniciará outra sessão.

## Revise os recursos de acessibilidade

Por fim, vamos revisar os recursos de acessibilidade criados com o agente personalizado de acessibilidade. Esta PR deve incluir o modo de alto contraste atribuído no Exercício 3 e o modo claro solicitado no Mission Control durante o Exercício 4.

1. Retorne ao repositório no GitHub.com.
2. Selecione a guia **Pull Requests**.
3. Selecione a PR com um título semelhante a **Add high contrast mode to website**.

> [!NOTE]
> Se o Copilot ainda estiver trabalhando na tarefa, a pull request terá o marcador **[WIP]**. Nesse caso, aguarde alguns minutos até que ele termine.

4. Selecione a guia **Files changed** para revisar o código criado.
5. Revise a implementação, prestando atenção especial a:
   - componentes de interface para alternar entre os modos.
   - uso do armazenamento local para manter as preferências.
   - alterações de CSS ou estilo para os modos de alto contraste e claro.
   - atributos de acessibilidade (rótulos ARIA, navegação pelo teclado etc.).
   - código JavaScript/TypeScript que gerencia a alternância de modos.

6. Depois de revisar as atualizações, retorne à guia **Conversation** e role a página para baixo.
7. Você deverá ver um indicador de que alguns fluxos de trabalho aguardam aprovação.
8. Se houver fluxos aguardando aprovação, selecione **Approve and run workflows**.

   ![Aprovar e executar fluxos de trabalho](../../../_images/shared-approve-workflows.png)

9. Os fluxos deverão entrar na fila da seção de verificações da pull request. Se tudo correr bem, as verificações do projeto para o aplicativo Astro único serão aprovadas. Isso pode levar alguns minutos.
10. **Opcional:** alterne para esse branch no Codespace para testar os recursos de acessibilidade. Acesse o Codespace, abra o terminal e execute os comandos a seguir (substitua `<branch-name>` pelo nome do branch criado pelo Copilot):

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

    Depois, inicie o aplicativo e teste os controles dos modos de alto contraste e claro no navegador. Confirme se funcionam e se as preferências persistem após recarregar a página.

Observe como o agente personalizado de acessibilidade orientou o Copilot a implementar esses recursos seguindo práticas recomendadas de acessibilidade. Se encontrar problemas ou melhorias possíveis, mencione **@copilot** em um comentário para solicitar alterações, como nas PRs anteriores.

## Exercício opcional — continue delegando

O agente na nuvem é mais útil quando você pode delegar itens reais do backlog e trabalhar em outra coisa. Para praticar, crie mais algumas issues no repositório e atribua-as ao Copilot. Por exemplo:

- criar um formulário de interesse de apoiadores na página de detalhes de um jogo.
- implementar paginação na lista de jogos.
- adicionar validação de entrada e tratamento de erros aos auxiliares de acesso a dados.

## Resumo

Você concluiu o fluxo de trabalho do agente na nuvem. Nestas lições, você:

- **Inspecionou os arquivos de instruções personalizados incluídos no repositório** para observar mais tarde seu efeito nos resultados do agente na nuvem.
- **Atribuiu issues ao agente na nuvem do Copilot** e acompanhou a configuração do ambiente, o planejamento e a execução assíncrona.
- **Criou e usou um agente personalizado** para acessibilidade, adicionando controles para os modos de alto contraste e claro.
- **Usou a página de agentes do Copilot como Mission Control** para monitorar e orientar a sessão de acessibilidade.
- **Revisou e refinou as pull requests do agente na nuvem**, mencionando `@copilot` para solicitar alterações e aprovando fluxos de trabalho.

## Revisão e próximos passos

Você concluiu o fluxo de trabalho do agente na nuvem. Os outros ambientes complementam o que você praticou:

- 🖥️ **[Fluxo de trabalho do VS Code](../../vscode/)** — explore o modo de agente do Copilot Chat e a integração com MCP diretamente no IDE.
- 💻 **[Fluxo de trabalho do CLI](../../cli/)** — entregue duas alterações revisadas no terminal com os modos Plan e Autopilot, skills de agente, um agente de QA personalizado, Playwright MCP, Agent Merge e a integração opcional `/delegate` com o agente na nuvem.

No seu repositório, experimente estas ideias:

- Atribua ao agente na nuvem uma issue de refatoração ou de cobertura de testes.
- Crie um agente personalizado para outro domínio.
- Configure `copilot-setup-steps.yml` para outra pilha de tecnologias.

## Recursos

- [GitHub Copilot][github-copilot]
- [Sobre agentes do Copilot][copilot-agents]
- [Atribuir issues do GitHub ao Copilot][assign-issue]
- [Práticas recomendadas para o fluxo de configuração do agente na nuvem do Copilot][cloud-agent-best-practices]
- [Configurar o firewall do agente na nuvem do Copilot][agent-firewall]

---

| [← Lição anterior: Gerenciar agentes][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall

[previous-lesson]: ../4-managing-agents/
