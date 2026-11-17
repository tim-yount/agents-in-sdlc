---
title: "演習 2 - Copilot エージェントモードで機能を追加する"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

アプリケーションの簡単な更新でも、複数のファイル変更やテストの実行が必要になることがあります。開発者は通常、必要なファイルを探し、変更を加え、テストを実行し、問題をデバッグし、変更漏れのファイルを見つけて再度更新します。作業は際限なく続くことがあります。

そのようなときに役立つのが Copilot エージェントモードです。

エージェントモードは IDE でより自律的に作業できるように設計されています。プロジェクト構成を調べ、必要な変更を行い、テストなどのタスクを実行し、見つかった問題を自動的に修正します。エージェントモードでサイトに機能を追加する方法を確認しましょう。

> [!NOTE]
> 名前は似ていますが、エージェントモードとクラウドエージェントは異なる用途向けに作られています。エージェントモードは IDE 内で動作し、すばやいフィードバックと対話を可能にします。クラウドエージェントはチームメンバーのように非同期で作業し、イシューやプルリクエストを通じてやり取りします。

この演習では、次のことを学びます。

- Copilot エージェントモードでプロジェクトを調べ、関連ファイルを特定し、複数ファイルにまたがる変更を行う方法。
- GitHub Copilot エージェントモードで UI とデータレイヤーに新機能を実装する方法。
- Copilot エージェントモードが生成した変更とテストをレビューしてからコードベースにマージする方法。

## シナリオ

ゲームの一覧が増えてきたため、カテゴリと出版社で絞り込めるようにします。前の演習で出版社ヘルパーを追加しました。次に Copilot エージェントモードを使って、残りのデータレイヤー、UI、テストを完成させます。

## Tailspin Toys の Web サイトを実行する

変更を加える前に、Tailspin Toys の現在の機能を確認します。

この Web サイトは、開発者をテーマにしたボードゲーム向けクラウドファンディングプラットフォームです。ゲームの一覧と詳細を表示します。サイトは単一の Astro アプリで、ビルド時に静的 HTML を生成します。ページはフロントマターから Drizzle ORM を使ってローカルの SQLite データベースを直接参照するため、独立したバックエンド API やクライアント側 UI フレームワークはありません。再利用可能なデータアクセスヘルパーは `src/lib/` に置き、操作性は標準 DOM API を使う小規模な Astro `<script>` で追加します。

### Web サイトを起動する

`npm run dev` タスクを使うと、単一の Astro 開発サーバーを起動できます。GitHub Codespace で次の手順を実行します。

1. Codespace に戻ります。前の演習の後、`main` ブランチにいるはずです。
2. Codespace 内で <kbd>Control</kbd>+<kbd>`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux) を押して、新しいターミナルを開きます。
3. フィルター機能の作業用ブランチを作成して切り替えます。

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. 次のコマンドを実行してサイトを起動します。

   ```bash
   npm run dev
   ```

   Astro 開発サーバーが起動すると、次のような URL が表示されます。

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> `http://localhost:4321` を開くかどうかを尋ねるダイアログが表示された場合は、**x** を選択して閉じます。

5. <kbd>Command</kbd> (Mac) または <kbd>Ctrl</kbd> (Windows/Linux) を押しながら、ターミナルに表示された Astro サーバーのアドレス `http://localhost:4321` を選択して、サイトを開きます。

> [!NOTE]
> Codespace のターミナルで localhost URL を選択すると、`https://<your-codespace-name>-4321.app.github.dev/` に自動的に転送されます。これは Codespace 内の Web サーバーをホストするためのプライベートトンネルです。

### Web サイトを確認する

サイトを起動したら、機能を確認できます。主な機能は次のとおりです。

- **ホームページ**: ボードゲームのタイトル、画像、説明を一覧表示します。
- **ゲーム詳細ページ**: ゲームを選択すると、タイトル、説明、出版社、カテゴリなどの詳細が表示されます。

## Copilot でバックログを確認する

> [!TIP]
> **Copilot Chat を開く**
>
> 次の演習を始める前に Codespace に戻り、Copilot Chat パネルを開き、**New Chat** を選択して新しい会話を始めます。モードとモデルの選択は演習ごとに異なります。必要な場合は、手順の中で説明します。

サイトの初期実装は動作しますが、新しい機能を追加して改善します。まずバックログを確認しましょう。テンプレートからプロジェクトをセットアップしたときにイシューのバックログも自動作成されています。GitHub Copilot に項目を表示してもらいます。

1. Chat ビューのエージェントドロップダウンから **Agent** を選択します。**Agent** は自律的に計画し、複数のファイルを変更し、ターミナルコマンドを実行し、ツールを呼び出します。

   ![Chat ビューのエージェント選択メニュー](../../../_images/shared-chat-mode-selector.png)

2. 利用可能なモデル一覧から **Claude Sonnet 4.5** を選択します。

> [!CAUTION]
> ワークショップの作成者が特定のモデルを推奨するものではありません。ワークショップの作成時に Claude Sonnet 4.5 を使用したため、手順で指定しています。参加者の体験を揃えるため、比較的一貫したコード提案を期待しています。ただし、LLM の出力は確率的なため、ワークショップに記載したものと異なる提案が出ることがあります。これは通常の動作です。

> [!NOTE]
> LLM の確率的な性質により、Copilot が別の MCP コマンドを使う場合がありますが、タスクは同様に完了できます。

3. 次のプロンプトを Copilot に送信して、バックログのイシューについて尋ねます。

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

4. **Continue** を選択して、すべてのイシューを一覧表示するコマンドを実行します。
5. 生成されたイシュー一覧を確認します。

Copilot は、ユーザーに最も役立つと考える項目を基準に、優先順位も付けています。

## 指示ファイルを確認する

エージェントにコードを生成させる前に、作業のコンテキストを Copilot に伝える指示ファイルを確認します。Web サイトに機能を追加する方法を説明する [ユーザーインターフェイス (UI) の指示ファイル](https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md)を使います。

1. Codespace で `.github/instructions/ui.instructions.md` を開きます。
2. 機能を追加するための全体的なガイダンスを確認します。次の内容が含まれます。
   - アーキテクチャの概要。
   - コンポーネントの設計、テスト容易性、アクセシビリティの原則。
   - Astro、Tailwind CSS、Drizzle などのファイル種類ごとの指示ファイルへのリンク。

> [!TIP]
> 指示ファイルから、ほかの指示ファイルやプロジェクト内のファイルを参照できます。パスは指示ファイルからの相対パスです。指示を再利用し、複雑な内容を管理しやすい単位に分け、例やテンプレートを示せます。

## フィルター機能を実装する

フィルター機能を完成させるには、少なくとも次の 3 つの変更が必要です。

- データレイヤー (`src/lib/`) に残りのフィルターロジックを追加または改善する。
- フィルターの動作をテストするテストを追加または更新する。
- ゲーム一覧ページにフィルター UI を追加する。

さらに、コードベースにマージする前にテストが成功する必要があります。Copilot エージェントモードに作業を依頼しましょう。

1. Copilot との現在の会話を続けるか、**New Chat** を選択して新しく始めます。
2. **Add Context**、**Instructions**、**ui** の順に選択して、指示ファイルを追加します。

   ![UI 指示ファイルを選択する例](../../../_images/ex3-select-instructions-file.png)

3. Chat ビューのエージェントドロップダウンで **Agent** が選択されていることを確認します。

   ![Chat ビューのエージェント選択メニュー](../../../_images/shared-chat-mode-selector.png)

4. モデルが **Claude Sonnet 4.5** のままであることを確認します。
5. バックログ内の関連イシューを基に機能を実装するよう、次のプロンプトを送信します。

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

6. Copilot がプロジェクトを調べ、目的の機能に関連するファイルを探す様子を確認します。データレイヤーのヘルパー、UI、テストを見つけてから、ファイルを変更し、テストを実行します。

   ![Copilot がプロジェクトファイルを調べる画面](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> Copilot はプロジェクトの調査、ファイルの編集、テストの実行など複数の作業を行います。タスクやコードベースの複雑さによっては、数分かかることがあります。その間、エディターに **Keep** と **Undo** ボタンが表示される場合があります。作業中に選択する必要はありません。完了後、すべての変更に対して **Keep** または **Undo** を選択できます。

7. Copilot に求められたら **Continue** を選択し、テストを実行します。

   ![Copilot Chat のテスト実行確認ダイアログ](../../../_images/ex3-agent-mode-run-tests.png)

8. 作業中に待ち時間が発生したり、テストが失敗したりすることがあります。問題ありません。Copilot はタスクが完了し、エラーが見つからなくなるまで、コード生成とテストを繰り返します。

   ![Copilot エージェントモードの完了した Chat セッション](../../../_images/ex3-agent-mode-proposed-changes.png)

9. 生成されたコードに問題がないか確認します。

> [!CAUTION]
> Copilot やほかの AI ツールが生成したコードは、必ずレビューしてください。

10. Web サイトを開いているブラウザーに戻り、新しい機能を確認します。
11. 動作とコードを確認したら、Copilot Chat ウィンドウで **Keep** を選択します。

## まとめと次のステップ

GitHub Copilot エージェントモードを使って、Tailspin Toys の Web サイトに新機能を追加する方法を確認しました。次のことを学びました。

- GitHub Copilot エージェントモードで UI とデータレイヤーに新機能を実装する方法。
- Copilot エージェントモードでプロジェクトを調べ、関連ファイルを特定し、複数ファイルにまたがる変更を行う方法。
- Copilot エージェントモードが生成した変更とテストをレビューしてからコードベースにマージする方法。

次は [Playwright MCP サーバーで機能をテスト][next-lesson]し、プルリクエストを作成します。

### ボーナス演習 — ページ分割を実装する

ゲームの一覧が増えると、ページ分割が必要になります。この演習で学んだことを使い、Copilot にページ分割を実装するよう依頼します。次の点を検討してください。

- 指示ファイルを使うなど、既存のベストプラクティスに従います。
- ユーザーがページサイズを選べるようにするか、固定値にするかを決めます。
- 希望する実装に必要なガイダンスを、プロンプトに含めます。
- Copilot にコンテキストを伝え、変更を依頼しながら反復する必要がある場合があります。これが Copilot を使うときの通常の進め方です。

## リソース

- [Copilot の ask、edit、agent モード: 機能と使い分け][choose-mode]
- [VS Code のエージェントモード][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
