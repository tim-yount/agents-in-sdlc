---
title: "レッスン 12 - GitHub Pages でサイトをデプロイする"
description: "GitHub Copilot アプリを使って Pages ワークフローを設定し、プルリクエストをレビューして、公開された Space Quiz を確認します。"
authors:
  - jamesmontemagno
lastUpdated: 2026-10-12
---

GitHub Pages でデプロイして、Space Quiz を一般公開しましょう。Copilot はワークフローの準備とデプロイの案内を行いますが、変更をレビューし、サイトが公開されたことを確認するのはユーザーの責任です。

このレッスンでは、次のことを行います。

- Copilot に GitHub Pages のデプロイ設定を依頼します。
- マージ前にワークフローとプルリクエストをレビューします。
- デプロイの手順に従い、公開されたサイトを確認します。

## シナリオ

Space Quiz はすでに GitHub リポジトリにありますが、まだ簡単に試せる方法がありません。単一ファイルのサイトを GitHub Pages で公開すれば、サーバーやランタイムの依存関係を追加せずに、公開 URL から利用できるようになります。

## Copilot にデプロイの準備を依頼する

> [!WARNING]
> プルリクエストを作成すると、コードがコミットおよびプッシュされることがあります。プロンプトを送る前に、承認設定と送信先のリポジトリを確認してください。**すべて承認**に設定している場合、別途確認を求められるとは限りません。

`space-quiz` の Copilot アプリのセッションで、次のプロンプトを送信します。

```plaintext
Prepare a GitHub Pages deployment for this repository. Create a GitHub Actions workflow that builds the website if needed and deploys it to GitHub Pages after changes reach the default branch. Add a README describing the app and how to run it locally if one does not already exist. Create a pull request with these changes and report its link and any required Pages settings or permissions. Do not merge, enable auto-merge, change Pages settings, or deploy. Stop and wait for my review.
```

## ワークフローとプルリクエストをレビューする

1. README は、リポジトリにまだ存在しない場合にのみ追加されていることを確認します。
2. ビルドとデプロイの手順、トリガー、権限を含め、プルリクエストの変更をレビューします。
3. ワークフローが、マージ前のプルリクエストではなくデフォルトブランチからデプロイすることを確認します。
4. 修正が必要な場合は依頼し、更新された差分をレビューします。マージを許可する前に、必須のプルリクエストチェックが成功するまで待ちます。

## マージとデプロイを許可する

> [!WARNING]
> 次のプロンプトを送信すると、レビュー済みプルリクエストのマージ、リポジトリの Pages 設定の変更、サイトの公開をエージェントに許可することになります。レビューを完了し、リポジトリとプルリクエストを確認してから送信してください。承認設定によっては、これらの操作が別の確認なしに実行されることがあります。

`<PR_NUMBER>` をレビューしたプルリクエストの番号に置き換えてから、別のプロンプトとして送信します。

```plaintext
I have reviewed pull request <PR_NUMBER> in this repository and authorize its merge and deployment. Enable GitHub Pages using GitHub Actions, merge that pull request only after required checks pass, and monitor the deployment until it succeeds. Report the final URL of the live website. If you lack permission to enable Pages or merge, tell me exactly what I need to approve or do; do not report success until the site is live.
```

![マージ済みの space-quiz プルリクエスト、Build website・Upload artifact・Deploy to Pages の各ステップが成功した GitHub Actions の Deploy website 実行結果、および yourname.github.io/space-quiz/ で公開された Space Quiz の3段階を示す図。](../../../_images/first-steps-app-pages-deploy.svg)

## デプロイを確認する

1. GitHub Actions のデプロイ実行が成功するまで確認します。
2. 報告された URL を開き、Space Quiz が表示されることを確認します。

エージェントが Pages の有効化やプルリクエストのマージを実行できない場合は、案内された具体的な手順に従ってください。デプロイが成功し、公開サイトが読み込まれるまで、タスクが完了したと判断しないでください。

## まとめと次のステップ

Space Quiz が公開され、エージェントの報告だけに頼らず、デプロイを確認できました。[レッスン 13: レビューと次のステップ][next-lesson]に進みましょう。

[next-lesson]: ../13-review/
