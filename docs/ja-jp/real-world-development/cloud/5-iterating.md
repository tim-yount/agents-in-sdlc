---
title: "演習 5: GitHub Copilot の作業を改善する"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 前のレッスン: エージェントの管理][previous-lesson] |
|:--|

## 作業をレビューする

このラボでは、ユーザーエクスペリエンスの改善と機能追加を目的に、GitHub Copilot に複数のタスクを依頼しました。コードへのドキュメント追加、デザインチームが改善を検討する関連ゲーム機能の作成、ハイコントラストモードとライトモードを含むアクセシビリティ機能の実装を依頼しました。コード変更を確認し、必要に応じて Copilot にフィードバックを伝え、作業を改善しましょう。

### シナリオ

生成 AI を利用しても、ソフトウェア設計と DevOps の基本は変わりません。生成されたコードは必ずレビューし、通常の DevOps プロセスに沿って作業します。チーム全員によるレビューを有効にする前に、ドキュメント、関連ゲーム機能、アクセシビリティ機能について GitHub Copilot が提案した変更を確認します。

## セキュリティと GitHub Copilot クラウドエージェント

Copilot クラウドエージェントは非同期かつ無人でタスクを実行するため、安全性を保つための制約があります。

- Copilot はリポジトリへの読み取りアクセスのみを持ち、書き込みアクセスはコード用ブランチに限られます。
- クラウドエージェントは GitHub Actions 内で実行され、作業用の独立した一時環境を作成します。
- GitHub Actions ワークフローの実行には、人間による承認が必要です。
- MCP サーバーを含む[外部リソースへのアクセスは、デフォルトで制限されています](https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall)。

## 生成されたドキュメントをレビューする

まず、コードへのドキュメント追加を依頼した GitHub Copilot クラウドエージェントの最初のプルリクエスト (PR) を確認します。GitHub.com の標準的な PR インターフェイスを使って作業します。

> [!NOTE]
> PR を開いたときに、GitHub Copilot がファイアウォールでブロックされているという警告が表示されることがあります。Copilot は、外部 MCP サーバーへの呼び出しを含む外部リソースへのアクセスをデフォルトで制限されているため、これは**想定どおりの動作**です。必要であれば、[Copilot クラウドエージェントのファイアウォールをカスタマイズまたは無効化][agent-firewall]できます。

1. github.com のリポジトリに戻ります。
2. **Pull Requests** を選択して、プルリクエスト一覧を開きます。
3. **Add missing documentation** などのタイトルが付いたプルリクエストを開きます。

> [!NOTE]
> Copilot がまだ作業中の場合、プルリクエストには **[WIP]** の表示があります。その場合は、Copilot が作業を終えるまで待ちます。数分かかることがあります。その間に休憩したり、これまでに学んだことを振り返ったりしてください。

4. 準備ができたら **Files changed** タブを選択し、変更をレビューします。

    ![Files changed タブ](../../../_images/shared-pr-files-changed.png)

5. TSDoc のドキュメントコメントや、その他のドキュメントが追加されたコードを確認します。具体的な変更内容は実行ごとに異なります。

    変更を確認しながら、演習 2 の最初に確認したカスタム指示ファイルから反映される TSDoc のコメント、TypeScript の規約、コメントヘッダーを探します。

6. 更新内容に問題がなければ **Conversation** タブに戻り、下にスクロールします。
7. ワークフローの承認待ちを示す表示を確認します。
8. ワークフローが承認待ちの場合は、**Approve and run workflows** を選択します。

   ![Approve and run workflows](../../../_images/shared-approve-workflows.png)

9. プルリクエストのチェック欄にワークフローが追加されます。問題がなければ、単一の Astro アプリのプロジェクトチェックが成功します。完了まで数分かかる場合があります。

## GitHub Copilot に変更を依頼する

Copilot とのプルリクエスト作業は一方通行ではありません。チームメンバーに依頼するのと同じように、プルリクエストやコードのインラインコメントで Copilot にメンションできます。Copilot はコメントを確認し、対応するセッションを開始します。結果は毎回異なるため、固定のプロンプトは指定できません。たとえば、次のような変更を依頼できます。

- 各コードファイルの先頭に、ファイルの概要を説明するコメントヘッダーを追加する。
- TypeScript ファイルと Astro ファイルに TSDoc のドキュメントコメントを追加する。
- Astro アプリの構成を説明する README を作成する。

1. **@copilot** をメンションして、生成されたドキュメントの変更をコメントで依頼します。上記の例を使うか、コードベースに必要な別のドキュメント改善を依頼してください。
2. **View Session** を選択し、Copilot が作業する様子を確認します。Copilot が変更用の新しいセッションを開始します。
3. **Back to pull request** を選択して PR に戻れます。

    ![プルリクエストに戻る](../../../_images/ex7-back-to-pr.png)

4. Copilot の作業が完了すると、プルリクエストに新しいコミットが表示されます。
5. **Files changed** タブを選択し、変更をレビューします。

満足するまで改善を依頼できます。問題がなければ、ドラフト PR をレビュー可能な状態にしてから、`main` ブランチにマージします。

![PR をレビュー可能な状態にする](../../../_images/ex7-ready-for-review.png)

## 関連ゲーム機能をレビューする

次に、ゲームの詳細ページに関連ゲームを表示するイシューに対して Copilot が作成した PR を確認します。

1. GitHub.com のリポジトリに戻ります。
2. **Pull Requests** タブを選択します。
3. **Show related games on the game details page** などのタイトルが付いた PR を選択します。
4. **Files changed** タブを選択して、生成されたコードをレビューします。
5. 更新内容に問題がなければ **Conversation** タブに戻り、下にスクロールします。
6. ワークフローの承認待ちを示す表示を確認します。
7. ワークフローが承認待ちの場合は、**Approve and run workflows** を選択します。

   ![Approve and run workflows](../../../_images/shared-approve-workflows.png)

8. プルリクエストのチェック欄にワークフローが追加されます。問題がなければ、単一の Astro アプリのプロジェクトチェックが成功します。完了まで数分かかる場合があります。
9. **任意:** Codespace でこのブランチに切り替えて、関連ゲーム機能を手動でテストすることもできます。Codespace に移動してターミナルを開き、`<branch-name>` を Copilot が作成したブランチ名（例: **copilot/fix-8**）に置き換えて、次のコマンドを実行します。

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

Copilot が関連ゲーム機能を作成しました。クラウドエージェントと反復しながら改善を依頼できます。たとえば、表示する関連ゲームの数を調整したり、コメントヘッダーや TSDoc のドキュメントコメントを追加したりできます（このタスクはカスタム指示を更新する**前**に割り当てたことを思い出してください）。前の PR と同様に、**Conversation** タブでコメントを追加すると、Copilot が確認して新しいセッションを開始します。

## アクセシビリティ機能をレビューする

最後に、アクセシビリティカスタムエージェントで実装した機能を確認します。この PR には、演習 3 で依頼したハイコントラストモードと、演習 4 でミッションコントロールから追加を依頼したライトモードの両方が含まれます。

1. GitHub.com のリポジトリに戻ります。
2. **Pull Requests** タブを選択します。
3. **Add high contrast mode to website** などのタイトルが付いた PR を選択します。

> [!NOTE]
> Copilot がまだ作業中の場合、プルリクエストには **[WIP]** の表示があります。その場合は、Copilot の作業が完了するまで数分待ちます。

4. **Files changed** タブを選択して、生成されたコードをレビューします。
5. 実装を確認し、特に次の点に注目します。
   - モード切り替え用の UI コンポーネント。
   - ユーザー設定を保持するためのローカルストレージの使用方法。
   - ハイコントラストモードとライトモードの CSS またはスタイルの変更。
   - ARIA ラベルやキーボード操作などのアクセシビリティ属性。
   - モードを切り替える JavaScript または TypeScript コード。

6. 更新内容に問題がなければ **Conversation** タブに戻り、下にスクロールします。
7. ワークフローの承認待ちを示す表示を確認します。
8. ワークフローが承認待ちの場合は、**Approve and run workflows** を選択します。

   ![Approve and run workflows](../../../_images/shared-approve-workflows.png)

9. プルリクエストのチェック欄にワークフローが追加されます。問題がなければ、単一の Astro アプリのプロジェクトチェックが成功します。完了まで数分かかる場合があります。
10. **任意:** Codespace でこのブランチに切り替え、アクセシビリティ機能を手動でテストできます。Codespace に移動してターミナルを開き、`<branch-name>` を Copilot が作成したブランチ名に置き換えて、次のコマンドを実行します。

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

    その後、アプリケーションを起動し、ブラウザーでハイコントラストモードとライトモードを切り替えます。ページを再読み込みしても設定が保持されることを確認してください。

アクセシビリティカスタムエージェントが、アクセシビリティのベストプラクティスに沿って機能を実装するよう Copilot を誘導したことを確認してください。アクセシビリティに関する懸念や改善点があれば、前の PR と同じようにコメントで **@copilot** に修正を依頼できます。

## 任意の演習 — 作業の委任を続ける

クラウドエージェントには、実際のバックログ項目を任せ、その間に別の作業を進める方法が適しています。この方法に慣れるため、リポジトリにイシューを追加して Copilot に割り当ててみましょう。次のようなタスクを依頼できます。

- ゲームの詳細ページに支援者向け問い合わせフォームを作成する。
- ゲーム一覧ページにページネーションを実装する。
- データアクセスヘルパーに入力検証とエラー処理を追加する。

## まとめ

クラウドエージェントのハーネスを完了しました。各レッスンを通して、次のことを行いました。

- **このリポジトリにあるカスタム指示ファイルを確認し**、後でクラウドエージェントが生成するコードへの影響を確認しました。
- **イシューを GitHub Copilot クラウドエージェントに割り当て**、環境のセットアップ、計画、非同期の作業を確認しました。
- **カスタムエージェントを作成して使用し**、アクセシビリティのためにハイコントラストモードとライトモードを追加しました。
- **Copilot エージェントページをミッションコントロールとして使用し**、実行中のアクセシビリティセッションを監視して誘導しました。
- **クラウドエージェントが作成したプルリクエストをレビューして改善し**、`@copilot` に変更を依頼して、ワークフローを承認しました。

## レビューと次のステップ

クラウドエージェントのハーネスを完了しました。引き続き学ぶ場合は、ほかのハーネスで今回の内容をさらに実践できます。

- 🖥️ **[VS Code ハーネス](../../vscode/)** — IDE で Copilot Chat のエージェントモードと MCP 統合を試します。
- 💻 **[CLI ハーネス](../../cli/)** — Plan モードと Autopilot モード、エージェントスキル、カスタム QA エージェント、Playwright MCP、Agent Merge、任意の `/delegate` によるクラウドエージェントとの連携を使い、ターミナルからレビュー済みの変更を 2 つ実装します。

自分のリポジトリでは、次のようなタスクを試せます。

- リファクタリングやテストカバレッジのイシューをクラウドエージェントに割り当てる。
- 別の分野向けのカスタムエージェントを作成する。
- 別の技術スタック向けに `copilot-setup-steps.yml` を設定する。

## リソース

- [GitHub Copilot][github-copilot]
- [Copilot エージェントについて][copilot-agents]
- [GitHub イシューを Copilot に割り当てる][assign-issue]
- [Copilot クラウドエージェントのセットアップワークフローに関するベストプラクティス][cloud-agent-best-practices]
- [Copilot クラウドエージェントのファイアウォールを設定する][agent-firewall]

---

| [← 前のレッスン: エージェントの管理][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall

[previous-lesson]: ../4-managing-agents/
