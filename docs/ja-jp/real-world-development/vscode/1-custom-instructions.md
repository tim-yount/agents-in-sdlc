---
title: "演習 1 - カスタム指示 (VS Code)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 前のレッスン: 前提条件][previous-lesson] · [次のレッスン: エージェントモード →][next-lesson]

生成 AI を使うときは、コンテキストが重要です。タスクを特定の方法で進める必要がある場合や、Copilot に知っておいてほしい背景情報がある場合は、そのコンテキストを参照できるようにします。Copilot にコード生成の指針を伝える方法はいくつかあります。その中心となる[指示ファイル][instruction-files]を使うと、作業の進め方を伝えられます。

この演習では、次のことを行います。

- リポジトリのカスタム指示とパスに応じた指示ファイルを使って、プロジェクト固有のコンテキスト、コーディングガイドライン、ドキュメント標準を Copilot に伝える方法を確認します。
- 既存の指示を適用して、フィルター機能の最初のデータ部分（出版社ヘルパー）を生成します。
- `.github/copilot-instructions.md` に、リポジトリ全体に適用する標準を追加します。
- 同じプロンプトを再実行し、生成コードが新しい標準に従うことを確認します。
- 指示の変更と機能の一部を `main` にコミットし、次の演習で新しい指示を使えるようにします。

> [!CAUTION]
> 生成コードが設定した標準から外れることがあります。Copilot の出力は決定論的ではありません。この演習では、指示の更新後に動作がどのように**変化する傾向にあるか**を確認します。出力が文字単位で同じになる必要はありません。

## 指示ファイル

### シナリオ

Tailspin Toys には、開発手法に関するガイドラインと要件があります。たとえば、次のようなものです。

- データレイヤーには必ずユニットテストを用意します。
- UI はダークモードにし、現代的な見た目にします。
- コードのドキュメントには TSDoc のドキュメントコメントを使用します。
- 各ファイルの先頭に、そのファイルの役割を説明するコメントブロックを追加します。

指示ファイルを使って、Copilot がこれらの開発手法に沿ってタスクを進めるために必要な情報を提供します。

### カスタム指示

カスタム指示を使うと、コーディングスタイルや要件に関するコンテキストと希望を Copilot に伝えられます。使用する規約やライブラリ、好みのコメント形式を指定することで、より適切な提案やコードを生成できるように誘導できます。リポジトリ全体、または特定の種類のファイルに適用する指示を作成できます。

指示ファイルには次の 2 種類があります。

- `.github/copilot-instructions.md` は、リポジトリに対する**すべての**リクエストで Copilot に送信される単一の指示ファイルです。Copilot Chat や CLI でのほとんどのリクエストに関係する、プロジェクトレベルの情報を記載します。技術スタック、開発対象の概要、ベストプラクティス、全般的なガイダンスなどが該当します。
- `.github/instructions/*.instructions.md` は、特定のタスクやファイルの種類に合わせて作成できます。TypeScript や Astro などの言語、UI コンポーネントの作成、ユニットテストの追加といったタスクのガイダンスを記載できます。

> [!NOTE]
> IDE で作業する場合、指示ファイルは Copilot Chat のコード生成にのみ使われ、コード補完や次の編集候補には使われません。
>
> Copilot Chat、Copilot CLI、Copilot クラウドエージェントは、リポジトリレベルの指示ファイルと、`applyTo` フロントマターを持つ `*.instructions.md` ファイルの両方をコード生成時に使用します。
>
> さらに Copilot は、AGENTS.md や CLAUDE.md など、別の規約に基づく指示ファイルにも対応しています。[対応する指示ファイルの形式][custom-instructions-support]を参照してください。

### 指示ファイルを管理するためのベストプラクティス

指示ファイルの作成方法をすべて説明することは、このワークショップの範囲外です。ただし、サンプルプロジェクトに含まれるファイルは一般的な方法を示しています。基本的には、次のようにします。

- `copilot-instructions.md` には、開発対象の説明、プロジェクト構成、全体的なコーディング標準など、プロジェクトレベルのガイダンスを記載します。
- `*.instructions.md` は、ユニットテスト、Astro コンポーネント、データレイヤーといったファイルの種類や、特定のタスク向けに使います。
- 自然な言葉で、明確なガイダンスとコードの例を示します。

指示ファイルに決まった唯一の形式はありません。AI の使い方と同じように、実際に試しながら、プロジェクトに適した方法を見つけてください。

> [!TIP]
> GitHub Copilot を使うプロジェクトには、充実した指示ファイル一式を用意することをお勧めします。このプロジェクトには、[UI 更新][ui-instructions]や [Astro][astro-instructions]など、さまざまなタスク向けのファイルがあります。
>
> Copilot に指示ファイルの生成を依頼することもできます。方法は利用する環境によって異なります（たとえば、VS Code の **Configure Chat → Generate Agent Instructions**、Copilot CLI の `/init` など）。必要な場合は、利用中の環境向けのレッスンで説明します。
>
> テンプレートや出発点を探していますか。[awesome-copilot][awesome-copilot]には、指示ファイル、カスタムエージェント、その他のリソースが多数あります。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## このプロジェクトのカスタム指示ファイルを確認する

このリポジトリにある指示ファイルを確認します。中心となる `copilot-instructions.md` と、さまざまなタスク向けの `*.instructions.md` ファイルがあります。エディターまたは GitHub の Web UI で開いてください。

1. `.github/copilot-instructions.md` を開きます。
2. プロジェクトの簡単な説明と、**Agent notes**、**Code standards**、**Scripts**、**Repository Structure** などのセクションを確認します。**Code standards** には **GitHub Actions Workflows** の指針も含まれています。これらは Copilot とやり取りするときに適用されます。
3. `.github/instructions` フォルダーを開いて内容を確認します。Astro ファイル、Drizzle データレイヤー、テストなどの指示があります。
4. `.github/instructions/unit-tests.instructions.md` を開きます。先頭の `applyTo` フィールドは、リポジトリルートからの相対パスで、指示が適用されるファイルを指定します。ここでは、たとえば `**/*.test.ts` に一致する TypeScript のテストファイルが対象です。
5. このプロジェクトでユニットテストを作成するときの指示を確認します。
6. 最後に `.github/instructions/drizzle.instructions.md` を開き、末尾までスクロールします。`unit-tests.instructions.md` などの指示ファイルや、プロジェクト内の既存ファイルへのリンクがあります。大きな指示を再利用可能な小さなファイルに分け、Copilot が参照できる例を示せます（ここに記載されたパスは、リポジトリルートではなく指示ファイルからの相対パスです）。

> [!NOTE]
> `copilot-instructions.md` の **Code formatting requirements** セクションではプロジェクトのコーディング標準を説明していますが、コード内ドキュメントの要件はまだありません。次の手順で、TSDoc のドキュメントコメントとファイル先頭のコメントヘッダーに関するルールを追加します。

## 変更用のブランチを作成する

ここではベストプラクティスに従い、作業用のブランチを作成します。

1. 前の演習で使用した Codespace に戻ります。
2. <kbd>Control</kbd>+<kbd>`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux) を押して、新しいターミナルを開きます。
3. 新しいブランチを作成して切り替えます。

   ```bash
   git checkout -b custom-instructions
   ```

## 指示を更新する前に Copilot Chat を使う

> [!TIP]
> **Copilot Chat を開く**
>
> 次の演習を始める前に Codespace に戻り、Copilot Chat パネルを開き、**New Chat** を選択して新しい会話を始めます。モードとモデルの選択は演習ごとに異なります。必要な場合は、手順の中で説明します。

カスタム指示の効果を確認するため、最初に現在の指示ファイルを使ってプロンプトを送信します。後で指示を更新した後、同じプロンプトを再送信して違いを確認します。

1. 前の演習で開いたエディタータブを閉じ、Copilot が必要なコンテキストだけを取得するようにします。
2. `src/lib/publishers.ts` を開き、ヘルパーを配置する場所を Copilot に示します。
3. Chat ビューのエージェントドロップダウンから **Agent** を選択し、Copilot がファイルを変更できるようにします。

   ![Chat ビューのエージェント選択メニュー](../../../_images/shared-chat-mode-selector.png)

4. 次のプロンプトを送信します。

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

5. Copilot はプロジェクトを調べて、ヘルパーファイルとテストを含むコードを更新します。
6. 提案されたヘルパーは、最初の引数として `db` クライアントを受け取り、型付きの出版社配列を返す関数です。これは `src/lib/*.ts` に適用される `.github/instructions/drizzle.instructions.md` のデータレイヤー規約に基づいています。
7. 提案コードに TSDoc のドキュメントコメントとファイル単位のコメントヘッダーが**ない**ことを確認します。

> [!CAUTION]
> Copilot の出力は確率的なため、指示しなくてもドキュメントコメントが追加される場合があります。その場合も問題ありません。この演習では、指示を更新した後に動作の一貫性が向上することを確認します。

## リポジトリの新しい標準を追加する

前述のとおり、`.github/copilot-instructions.md` は Copilot にプロジェクトレベルの情報を提供します。コーディング標準を追加し、提案の品質を高めましょう。

1. `.github/copilot-instructions.md` をもう一度開きます。
2. 27 行目付近にある **Code formatting requirements** セクションを探します。プロジェクトのコーディング標準が記載されていますが、コード内ドキュメントのルールはありません。そのため、生成されたヘルパーにドキュメントコメントが含まれていませんでした。
3. 既存の標準の直後に、次の Markdown 行を追加して、ファイルヘッダーと TSDoc のドキュメントコメントを Copilot に指示します。

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. `copilot-instructions.md` を保存します。

> [!TIP]
> 前のレッスンで見たように、指示ファイルは、すべてに適用する `.github/copilot-instructions.md` と、言語やファイルの種類、特定のタスクに適用する `*.instructions.md` のどちらにも作成できます。今回追加したドキュメントコメントのルールのように、プロジェクト全体の標準はリポジトリレベルのファイルに記載します。

## プロンプトを再実行して変化を確認する

1. Copilot Chat に戻り、**New Chat** を選択して会話を新しくします。
2. `src/lib/publishers.ts` を選択し、Copilot が対象ファイルに注目するようにします。
3. 前と**同じプロンプト**を送信します。

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

4. 提案ファイルの先頭に、次のようなコメントブロックが追加されていることを確認します。

   ```typescript
   /**
    * Publisher data-access helpers for the Tailspin Toys Crowd Funding platform.
    * Provides functions to retrieve publisher information from the database.
    */
   ```

5. 関数に、次のような TSDoc コメントが追加されていることを確認します。

   ```typescript
   /**
    * Returns a list of all publishers with their id and name.
    *
    * @param db - The Drizzle database client.
    * @returns A promise that resolves to an array of publisher objects.
    */
   ```

新しいプロジェクト標準を Copilot に伝え、次の演習で使うコードに適用できました。

## 指示をコミットしてブランチをプッシュする

指示ファイルもほかの資産と同じように、ソース管理で管理します。指示の更新とヘルパーの変更をリポジトリにコミットしてプッシュします。

1. <kbd>Control</kbd>+<kbd>`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux) を押して、新しいターミナルを開きます。
2. ターミナルで、指示とヘルパーの変更が含まれていることを確認します。

   ```bash
   git status
   ```

3. ターミナルで指示ファイルと、ヘルパーの基盤として Copilot が変更したファイルをステージしてコミットします。

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   # git status にテストなどの追加ファイルが表示された場合は、それらも追加します。
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

4. ブランチをリポジトリにプッシュします。

   ```bash
   git push -u origin custom-instructions
   ```

## プルリクエストを作成してマージする

ブランチをプッシュしたら、指示ファイルの変更に関するバックログのイシューに関連付けたプルリクエストを作成します。手動で作成する代わりに、GitHub ツールが接続されている Copilot に依頼します。イシューを探し、イシューをクローズする PR を作成するようプロンプトを送ります。

> [!NOTE]
> この演習では初めて Copilot に GitHub 上の操作を依頼します。プロジェクトのテンプレートでは、GitHub のツールがあらかじめワークスペースに接続されています。そのため、セットアップは不要です。Copilot が初めてツールを使うとき、VS Code から GitHub へのサインインを求められることがあります。指示に従って認証してください。後の演習では、この接続方法である Model Context Protocol について学びます。

1. Codespace で Copilot Chat を開きます。
2. <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd> (Windows/Linux) を押して Copilot Chat ビューを開き、エージェント選択メニューで **Agent** が選ばれていることを確認します。
3. 指示ファイルの更新と、新しい出版社ヘルパーの基盤を説明する PR を現在のブランチから作成するよう Copilot に依頼します。

   ```
   Find the issue related to updating the instructions file. Create a new PR from the current branch, highlight that the PR closes that issue, and include that we also added the publishers helper foundation for the upcoming filtering work.
   ```

4. Copilot がイシューを探して PR を作成します。
5. Copilot が GitHub 操作の実行を **Allow** するよう求めたら、コマンドを確認して必要に応じて許可します。
6. PR が作成されたら、次のプロンプトでマージを依頼し、ブランチを `main` に戻します。

   ```
   Merge the PR into main. Then return to main locally, and pull the latest code so we are up to date.
   ```

7. Copilot が GitHub 操作やシェルコマンドの実行を **Allow** するよう求めたら、コマンドを確認して必要に応じて許可します。

GitHub Copilot の支援でプルリクエストを作成し、マージできました。

## まとめと次のステップ

このプロジェクトの指示ファイルから Copilot がコンテキストを取得する方法を確認し、VS Code の Copilot Chat を使って次のことを行いました。

- コード生成のプロンプトを送り、*既存の*指示で Copilot が生成する内容を確認する。
- `.github/copilot-instructions.md` に新しい標準を追加する。
- 同じプロンプトを再実行し、提案コードに新しい標準が反映されることを確認する。
- 次の演習でコードを使えるように、指示の更新とヘルパーの基盤を `main` にコミットする。

次は、[エージェントモード][next-lesson]で指示を活用し、Copilot にコードベース全体にまたがる機能を追加してもらいます。

## リソース

- [GitHub Copilot のカスタマイズに使う指示ファイル][instruction-files]
- [カスタム指示を作成するためのベストプラクティス][instructions-best-practices]
- [Copilot 向けのカスタム指示を改善する 5 つのヒント][copilot-instructions-five-tips]
- [GitHub Copilot の個人用カスタム指示][personal-instructions]
- [指示ファイルのコレクションとその他のリソース: Awesome Copilot][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[personal-instructions]: https://docs.github.com/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
