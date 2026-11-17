---
title: "実践的な開発"
slug: ja-jp/real-world-development
authors:
  - geektrainer
lastUpdated: 2026-09-16
---

現実的なシナリオ、完成したアプリケーション、共有バックログを使って、ソフトウェア開発ライフサイクル全体で GitHub Copilot を活用しましょう。変更の計画、コードの作成、動作のテスト、プルリクエストのレビュー、エージェントによる作業管理を繰り返しながら進めます。

## シナリオ

あなたは、開発者向けテーマのボードゲーム向けクラウドファンディングを提供する架空の会社、Tailspin Toys に入社したばかりの開発者です。チームのバックログは GitHub イシューとして登録されており、すぐに取り組めます。フィルターやページネーションなどの機能開発に加えて、アクセシビリティやコーディング規約などの品質改善も含まれています。

## 開発環境を選ぶ

GitHub Copilot は、どの環境でも利用できます。開発方法に合った環境を選んでください。各ワークショップでは個別にセットアップを行い、共通の Tailspin Toys シナリオを使用します。

### [GitHub Copilot CLI][cli]

ターミナルでエージェント型アシスタントを使います。Plan モードと Autopilot モード、指示、スキル、カスタムエージェント、Playwright MCP、Agent Merge、実用的なスラッシュコマンドを扱います。

### [GitHub Copilot アプリ][app]

複数のエージェントセッションを並行して実行し、セッションモードを切り替え、キャンバスで共同作業し、デスクトップアプリで GitHub のイシューやプルリクエストを管理します。

### [GitHub Copilot クラウドエージェント][cloud]

GitHub のイシューを非同期エージェントに割り当て、作業を案内し、進行状況を監視して、作成されたプルリクエストをレビューします。

### [Visual Studio Code][vscode]

Visual Studio Code と GitHub Codespaces で GitHub Copilot を使います。エディターを離れずに、Copilot Chat のエージェントモード、MCP サーバー、カスタムエージェントを扱います。

[cli]: cli/
[app]: app/
[cloud]: cloud/
[vscode]: vscode/
