---
title: "レッスン 10 - まとめと次のステップ"
description: "Copilot CLI のワークフロー、2 つのプルリクエスト、再利用可能なカスタマイズ、追加リソースを振り返ります。"
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

GitHub Copilot CLI を使い、Tailspin Toys の開発ワークフローを最初から最後まで進めました。次のことを行いました。

- Codespace を準備し、Copilot CLI をインストールし、プロジェクトを確認して、登録済みのフィルター機能のイシューを見つけました。
- 星評価を追加し、転送されたブラウザーで結果をレビューして、最初のプルリクエスト (PR) を手動でマージしました。
- フィルター機能のイシューから開始し、Plan モードで方針を決め、Autopilot モードで作成して、Interactive モードでレビューしました。
- カスタム指示でエージェントを誘導し、既存の `quality-checks` スキルをカスタマイズして、ユニットテスト、lint、型チェックを実行しました。
- Playwright Model Context Protocol (MCP) サーバーを追加し、実際のブラウザーでフィルター機能を確認しました。
- 品質保証 (QA) カスタムエージェントを作成して選択し、要件、テストカバレッジ、スキルの結果、ブラウザーでの検証の根拠を評価しました。
- フィルター機能の変更全体をレビューし、フィルター機能の PR で Agent Merge を許可しました。
- コンテキスト、モデル、共有、任意のクラウドへの委任に使えるスラッシュコマンドを確認しました。

## 公開した内容

ワークショップには、更新された `main` からそれぞれ別のブランチで作成する 2 つの PR があります。

1. **星評価:** 既存の `starRating` と未評価状態をゲームカードに表示します。
2. **フィルターと品質ワークフロー:** フィルターを実装し、指示を更新して機能に適用し、`quality-checks` の報告をカスタマイズし、QA プロファイルを作成して関連テストを追加します。

フィルター機能の計画から PR 作成まで、同じ会話とブランチを使いました。ワークショップを簡潔にするため、作業を 1 つの PR にまとめています。

## さまざまな検証方法

自動テスト、自分でのブラウザー確認、MCP 経由の Copilot によるブラウザー確認など、複数の方法でコードを確認しました。`quality-checks` スキルはユニットテスト、lint、型チェックを実行し、新しい形式で報告しました。QA はこれらの結果と、要件およびテストカバレッジのレビューをまとめて、PR の前に報告しました。

追加するテストは実際の不足を補うものである必要があります。QA で新しいテストが不要と判断される場合もあります。マージを許可する前にコードと根拠をレビューし、変更後は関連する根拠を再確認してください。

## ベストプラクティス

Copilot に与えるコンテキストとツールが作業の結果を左右します。このワークショップでは、指示を更新し、スキルをカスタマイズし、QA プロファイルを作成し、MCP サーバーを構成しました。これらのカスタマイズは会話をまたいで再利用でき、チームの要件に合わせて調整できます。指示は標準を定め、スキルは繰り返し行う作業を説明し、カスタムエージェントは専門的な役割を定義し、MCP サーバーは外部ツールに接続します。エージェントの要約だけでなく、実際の変更とツールの結果をレビューしてください。

タスクに合った**モードとモデル**を選びます。作業前に方針を検討するには **Plan**、対象を絞った変更を進めながら確認するには **Interactive**、範囲の明確なタスクには **Autopilot** を使います。定型的な編集には高速なモデルを、複雑な作業にはより高性能なモデルを選びます。

インフラストラクチャと同じくらい、コンテキストも重要です。*何を*作りたいか、*なぜ*必要か、*どのように*作るかを明確に説明すると、結果が大きく変わります。

## さらに確認する

中心的なワークフローを学びました。Copilot CLI には、ほかにも次のような機能があります。

- `/review` でコードレビューエージェントに変更を分析してもらう。
- `/rubber-duck` で問題を話し合い、別の視点を得る。
- `/fleet` で独立したサブタスクを並行して調整する。
- `/worktree` で別のタスクを分離する。
- `/delegate` で Copilot クラウドエージェントにタスクを送る。

## 次のステップ

どのツールも、使い続けることが上達への近道です。本番コード、趣味のコード、何年も作ろうと思いながら手を付けていなかった小さなアプリなどで活用してください。チームと学びを共有し、メンバーの経験からも学びましょう。いつものように、ドキュメントも確認してください。

ターミナルから Tailspin Toys をさらに拡張したい場合は、任意の [Foundry Backer Concierge シリーズ][foundry]に進みます。ほかの環境での内容を比較するには、[VS Code ワークショップ][vscode]、[GitHub Copilot アプリのワークショップ][app]、または[Copilot クラウドエージェントのワークショップ][cloud]を確認してください。

## リソース

- [GitHub Copilot CLI について][about-cli]
- [Copilot CLI コマンドリファレンス][cli-reference]
- [Copilot CLI をカスタマイズする][customize-cli]
- [Copilot CLI でプルリクエストを管理する][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
