---
title: "演習 1 - カスタム指示 (クラウドエージェント)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 前のレッスン: 前提条件][previous-lesson] · [次のレッスン: GitHub Copilot クラウドエージェント →][next-lesson]

生成 AI を使うときは、コンテキストが重要です。タスクを特定の方法で進める必要がある場合や、Copilot に知っておいてほしい背景情報がある場合は、そのコンテキストを参照できるようにします。[指示ファイル][instruction-files]を使うと、Copilot に「何を」するかだけでなく、「どのように」進めるかも伝えられます。

この演習では、次のことを行います。

- リポジトリのカスタム指示とパスに応じた指示ファイルを使って、プロジェクト固有のコンテキスト、コーディングガイドライン、ドキュメント標準を Copilot に伝える方法を確認します。
- `.github/copilot-instructions.md` に、リポジトリ全体に適用する標準を追加します。

> [!NOTE]
> VS Code および CLI のハーネスとは異なり、この演習ではプロンプトの実行前後を比較しません。GitHub Copilot クラウドエージェントは GitHub イシューに対して非同期で動作するため、リアルタイムで並べて効果を示すのが難しいためです。このハーネスの後半で、エージェントが作成するプルリクエストをレビューするときに、指示ファイルの影響を確認します。

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

指示ファイルの作成方法をすべて説明することは、このワークショップの範囲外です。ただし、サンプルプロジェクトに含まれるファイルは、一般的なアプローチを示しています。基本的には、次のようにします。

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
> `copilot-instructions.md` の **Code formatting requirements** セクションではプロジェクトのコーディング標準を説明していますが、コード内のドキュメントに関する要件はまだありません。次の手順で、TSDoc のドキュメントコメントとファイル先頭のコメントヘッダーに関するルールを追加します。

## リポジトリの新しい標準を追加する

次は、この演習で行う唯一の編集です。コード内に TSDoc のドキュメントコメントとファイル単位のコメントヘッダーを追加するルールを、プロジェクト全体に適用します。後の演習でイシューを割り当てると、クラウドエージェントがこのルールを参照します。

編集する前に、作業用のブランチを作成します。クラウドエージェントはイシューの対象ブランチから指示を読み取りますが、編集内容はブランチにコミットしておきます。

1. Codespace のターミナルで、新しいブランチを作成して切り替えます。

   ```bash
   git checkout -b custom-instructions-cloud
   ```

前述のとおり、`.github/copilot-instructions.md` は Copilot にプロジェクトレベルの情報を提供します。リポジトリのコーディング標準にルールを追加し、提案の品質を高めましょう。

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

## 指示の更新をコミット、プッシュ、マージする

クラウドエージェントは、イシューの対象ブランチにある指示ファイルを読み取ります。次の演習でイシューを Copilot に割り当てると、Copilot は `main` からブランチを作成します。クラウドエージェントが指示を参照できるように、変更を `main` に反映してください。

1. ステージしてコミットします。

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. ブランチをプッシュします。

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. github.com で `custom-instructions-cloud` から `main` に向けたプルリクエストを作成し、マージします。次の演習でイシューを割り当てると、クラウドエージェントはこの指示を参照します。

> [!TIP]
> このワークショップで `main` に直接作業したい場合は、ブランチ作成を省略して `main` にコミットしてもかまいません。ブランチを使う手順は、実際のプロジェクトでの作業方法を再現するためのものです。

## まとめと次のステップ

Copilot がこのプロジェクトの指示ファイルからコンテキストを取得する方法を確認し、`.github/copilot-instructions.md` にリポジトリ全体の標準を追加しました。このハーネスの残りの演習で、クラウドエージェントが作成するプルリクエストにその標準が反映されることを確認します。

次に、[最初のイシューを GitHub Copilot クラウドエージェントに割り当てます][next-lesson]。

## リソース

- [GitHub Copilot のカスタマイズに使う指示ファイル][instruction-files]
- [カスタム指示を作成するためのベストプラクティス][instructions-best-practices]
- [Copilot 向けのカスタム指示を改善する 5 つのヒント][copilot-instructions-five-tips]
- [指示ファイルのコレクションとその他のリソース: Awesome Copilot][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
