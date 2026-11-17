---
title: "演習 2 - GitHub Copilot クラウドエージェント"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 前のレッスン: カスタム指示][previous-lesson] |
|:--|

技術的負債に悩んでいない組織は、ほとんどないでしょう。未解決のセキュリティ問題、更新が必要なレガシーコード、実装する時間がなくバックログに残ったままの機能リクエストなどがあります。GitHub Copilot クラウドエージェントは、コードの更新や機能の追加といった作業を自律的に実行できます。作業が完了すると、人間の開発者がレビューできるドラフト PR を作成します。これにより、面倒な作業を任せて開発プロセスを加速し、開発者はより大きな課題に集中できます。

GitHub Copilot クラウドエージェントを使って、次のことを確認します。

- コードを生成する環境をカスタマイズする。
- 操作が安全に行われるようにする。
- イシューの範囲を明確に定めることの重要性を理解する。
- イシューを Copilot に割り当てる。

## シナリオ

Tailspin Toys には対処したい技術的負債があります。最初のサイトを作った契約開発者は、ドキュメントを十分に整備しませんでした。まず、アプリケーションのエクスポートされたすべての関数に TSDoc のドキュメントコメントを追加します。

また、デザインチームはゲームを見つけやすくしたいと考えています。各ゲームの詳細ページに、同じカテゴリのほかのゲームを表示すれば、ユーザーはゲームを続けて探せます。まだ完成度の高い実装は必要なく、UX の受け入れテストに使えるものを求めています。この作業は現在ブロッカーですが、優先度の高いイシューがほかにあります。

このようなタスクは、優先順位が下がりやすい一方で、GitHub Copilot クラウドエージェントに適しています。Copilot に非同期で作業を任せれば、開発者は別の作業に集中し、後から戻って成果をレビューできます。

## GitHub Copilot クラウドエージェントを知る

[GitHub Copilot クラウドエージェント](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent)は、人間の開発者と同じようにバックグラウンドで作業を実行できます。人間の開発者と同様に、[GitHub イシューを Copilot に割り当てる](https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions)など、複数の方法で依頼できます。割り当てると、Copilot は進捗を記録するドラフトプルリクエストを作成し、環境をセットアップして、タスクに取りかかります。セッションは実行中でも完了後でも確認できます。提案された解決策のレビュー準備ができると、プルリクエストで通知されます。

## 範囲を明確にした指示の重要性

GitHub Copilot に魔法はありません。考える作業を省略できるわけではありません。一見簡単そうな作業でも、詳しく調べると複雑な場合があります。[Copilot クラウドエージェントに依頼するタスクの範囲][cloud-agent-best-practices]を慎重に決めてください。AI ペアプログラマーとして扱い、段階的に進め、学び、試し、適応させます。生成 AI を導入しても、ソフトウェア開発の基本は変わりません。

## このリポジトリのカスタム指示

前の演習では、カスタム指示と Copilot への指示方法を確認しました。カスタム指示の実習を終えていれば、`.github/copilot-instructions.md` の動作を確認したはずです。まだの場合は、ここで簡単に確認しましょう。Copilot クラウドエージェントに作業を割り当てる前に、このリポジトリにある指示ファイルを読み取り専用で確認すると、後からその影響を見つけやすくなります。

リポジトリの GitHub Web UI、または起動済みの Codespace で次のファイルを開きます。

- `.github/copilot-instructions.md` - **Code standards** セクションを確認します。特に TypeScript の規約と TSDoc のドキュメントコメントに関する要件に注目してください。
- `.github/instructions/unit-tests.instructions.md` - `applyTo` フロントマターを確認します。この指示は `**/*.test.ts` ファイルに適用されます。

次のセクションで `Code lacks documentation` イシューをクラウドエージェントに割り当てるとき、作成されたプルリクエストで、これらの指示ファイルに含まれる TSDoc のドキュメントコメント、TypeScript の規約、コメントヘッダーを確認してください。後の演習で PR をレビューするときにも、改めて説明します。

## GitHub Copilot クラウドエージェントの開発環境をセットアップする

誰がコードを書く場合でも、通常は必要な開発環境があり、作業前にスクリプトを実行して準備します。Copilot にタスクを割り当てる場合も同じです。Copilot は SWE と同じような方法で作業を行います。

クラウドエージェントは作業時に [GitHub Actions][github-actions] を使用します。作業を開始する前に実行する[セットアップワークフロー][setup-workflow]を `.github/workflows/copilot-setup-steps.yml` に作成すると、環境をカスタマイズできます。これにより、必要な開発ツールと依存関係を使用できるようになります。このラボの進行を助け、学習に集中できるよう、必要な設定は事前に済んでいます。Node.js、プロジェクトの依存関係、エンドツーエンドテスト用のブラウザーバイナリ、および単一の Astro アプリ用にマイグレーションとシードを済ませた SQLite データベースを利用できます。

```yaml
name: "Copilot Setup Steps"

# リポジトリの "Actions" タブからセットアップ手順をテストできます
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # *この手順*に必要な最小限の権限を設定します。Copilot には操作用の独自のトークンが付与されます。
    permissions:
      # 依存関係のインストールなど、セットアップ手順の一部としてリポジトリをクローンする場合は、`contents: read` 権限が必要です。セットアップ手順でクローンしない場合は、手順の完了後に Copilot が自動的にクローンします。
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # フロントエンド / アプリのセットアップ - Node.js (アプリ全体が Astro + Drizzle/libSQL になりました)
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

      # ビルドとテストでデータを利用できるように、ローカルの SQLite データベースをマイグレーションしてシードします。
      - name: Set up the database
        run: npm run db:setup
```

一般的な GitHub ワークフローファイルと同じですが、いくつか重要な点があります。

- `copilot-setup-steps` という単一のジョブが含まれています。このジョブは、Copilot がプルリクエストの作業を始める前に GitHub Actions で実行されます。
- `workflow_dispatch` トリガーを使うと、リポジトリの **Actions** タブからワークフローを手動実行できます。Copilot の実行を待たずに、ワークフローが正常に動くかテストできます。

## ドキュメントを追加する

ドキュメントの重要性は広く理解されていますが、情報が古い、またはドキュメントがないプロジェクトも少なくありません。このような技術的負債を放置すると、生産性が下がり、コードベースの保守や新しいチームメンバーの受け入れが難しくなります。Copilot はドキュメント作成を得意としているため、クラウドエージェントに依頼するのに適したタスクです。バックグラウンドで必要なドキュメントを作成します。後の演習で成果をレビューします。

1. 新しいブラウザータブで github.com のリポジトリを開きます。
2. **Issues** タブを選択します。
3. **New issue** を選択して、新しいイシューのダイアログを開きます。
4. **Blank issue** を選択してイシューを作成します。
5. **Title** に `Code lacks documentation` と入力します。
6. **Description** に次の内容を入力します。

    ```plaintext
    Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
    ```

7. **Create** を選択してイシューを作成します。
8. 右側の **Assign to Copilot** を選択して割り当てダイアログを開きます。

  ![Copilot をイシューに割り当てる](../../../_images/shared-assign-copilot.png)

9. **Assign** を選択します。
10. **Pull Requests** タブを選択します。
11. 新しく作成されたプルリクエスト (PR) を開きます。タイトルは `[WIP]: Code lacks documentation` のようなものです。一覧に表示されない場合は、少し待ってからブラウザーを更新してください。
12. 数分後、Copilot が To Do リストを作成したことを確認します。

> [!NOTE]
> Copilot の To Do リストが PR に表示されるまで数分かかることがあります。Copilot は環境を作成し（前述のワークフローを実行します）、プロジェクトを分析して、問題に取り組む方法を検討しています。

13. リストと、実行予定のタスクを確認します。
14. プルリクエストのタイムラインを下にスクロールし、Copilot がイシューの作業を開始したことを示す更新を確認します。
15. **View session** ボタンを選択します。

  ![Copilot のセッションビュー](../../../_images/ex4-view-session.png)

> [!CAUTION]
> 表示が更新されない場合は、ウィンドウを更新してください。

16. ライブセッションをスクロールし、Copilot がどのように問題を解決しているか確認します。コードを調べて状態を理解し、適切な計画を考え、コードを作成する様子を確認できます。

この作業には数分かかる場合があります。GitHub Copilot クラウドエージェントの主な目的の 1 つは、タスクを非同期に実行し、開発者が別の作業に集中できるようにすることです。この機能を活用するため、もう 1 つのタスクもクラウドエージェントに割り当て、その間にアプリケーションの機能追加に取り組みます。

## ゲームの詳細ページに関連ゲームを追加する

GitHub Copilot クラウドエージェントの大きな利点の 1 つは、作業を分担できることです。デザインチーム向けに関連ゲームのセクションを追加する作業自体は長くかからないかもしれませんが、その時間を別の作業に使えます。クラウドエージェントに割り当てましょう。

1. github.com のリポジトリに戻ります。
2. **Issues** タブを選択します。
3. **New issue** を選択して、新しいイシューのダイアログを開きます。
4. **Blank issue** を選択して、空のテンプレートを使います。
5. **Title** に `Show related games on the game details page` と入力します。
6. **Description** に次の内容を入力します。

    ```markdown
    We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
    ```

7. **Create** を選択してイシューを作成します。
8. 右側の **Assign to Copilot** を選択して割り当てダイアログを開きます。

  ![Copilot をイシューに割り当てる](../../../_images/shared-assign-copilot.png)

9. **Assign** を選択します。

まもなく、Copilot が作業を開始したことを示す 👀 がイシューの最初のコメントに表示されます。

![イシューで Copilot が作業中であることを示す目の絵文字](../../../_images/ex4-issue-eyes-emoji.png)

Copilot は 2 つ目の依頼に取り組んでいます。GitHub Copilot クラウドエージェントは SWE と同じように作業するため、常に監視する必要はありません。完了後にレビューできます。次は、カスタムエージェントの作成と使用を確認しましょう。

## まとめと次のステップ

このレッスンでは、[GitHub Copilot クラウドエージェント][copilot-agents]について学びました。クラウドエージェントにイシューを割り当てると、非同期に作業を進められます。技術的負債への対処、新機能の作成、別のフレームワークへのコード移行などを依頼できます。

このレッスンでは、次のことを確認しました。

- コード生成環境をカスタマイズする。
- 操作が安全に行われるようにする。
- イシューの範囲を明確に定めることの重要性を理解する。
- イシューを Copilot に割り当てる。

クラウドエージェントがバックグラウンドで作業している間に、カスタムエージェントの作成と使用を確認しましょう。[Copilot クラウドエージェントは MCP サーバー][cloud-agent-mcp]も使用できます。また、前のモジュールで確認したカスタム指示も利用できます。

## リソース

- [Copilot クラウドエージェントについて][copilot-agents]
- [GitHub イシューを Copilot に割り当てる][assign-issue]
- [Copilot クラウドエージェントのセットアップワークフローに関するベストプラクティス][cloud-agent-best-practices]

| [次のレッスン: カスタムエージェント →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
