# Claude Code コーディングアシスタント

Claude Codeでコードレビューを自動化するプラグインです。

## 特徴
- **自動コードレビュー**: GitHub CLIを使用してPRを分析し、体系的なレビューを実行
- **PR記載レビュー**: PRタイトル・説明文・テンプレート準拠をチェックし、ドキュメント品質を向上
- **Codex連携**: Codex MCPサーバによるマルチエージェント検証で高品質なレビューを実現
- **体系的分析**: PRテンプレートに基づく統一されたレビュー観点
- **GitHub統合**: レビューコメントを直接GitHubに投稿

---

## 🚀 インストール

### 1. マーケットプレイスを追加
```
/plugin marketplace add https://github.com/emuemuJP/claude-coding-assistant 
```

### 2. プラグインをインストール
```
/plugin install coding-assistant@emuemuJP/claude-coding-assistant
```

### 3. Claude Code を再起動

### 4. テスト
```
/coding-assistant:code-reviewer PR#123をレビューしてください
```

---

## 📝 使い方

### コードレビュー
```
/coding-assistant:code-reviewer PR#<番号>をレビューしてください
```

プラグインは以下の処理を自動実行：
1. PR情報の取得と分析
2. ファイル別の詳細レビュー
3. Codexによる妥当性検証（オプション）
4. GitHubへのコメント投稿
5. レビューサマリーの作成

### PR記載レビュー
```
/coding-assistant:pr-description-reviewer PR#<番号>をレビューしてください
```

PRのコードではなく、記載内容（タイトル、説明文、テンプレート準拠）をレビュー：
1. PRタイトルの明確さ・簡潔さをチェック
2. 説明文の目的・背景・影響範囲を評価
3. PRテンプレート必須項目の記入漏れを検出
4. テスト計画・関連Issue・スクリーンショットの有無を確認
5. 具体的な改善例を提示してGitHubにコメント投稿

### 前提条件
- GitHub CLI（gh）がインストール・認証済みであること
- codex MCPサーバが利用可能な場合、より高品質なレビューが可能

---

## 🔧 MCP サーバー設定

このプラグインはCodex MCPサーバを使用します。設定は`.claude-plugin/plugin.json`に含まれています。

```json
{
  "name": "coding-assistant",
  "mcpServers": {
    "codex": {
      "type": "stdio",
      "command": "codex",
      "args": ["mcp-server"]
    }
  }
}
```

### 前提条件
- `codex`コマンドがインストール済みであること
- インストール方法: [Codex公式ドキュメント](https://docs.codexmcp.dev/)
- プラグインのMCPサーバーを有効にするには **Claude Codeの再起動が必要** です

---

## 📁 ファイル構成

```
claude-coding-assistant/
├── .claude-plugin/
│   ├── plugin.json          # プラグイン設定（MCP設定含む）
│   └── marketplace.json     # マーケットプレイス設定
├── commands/
│   ├── code-reviewer.md     # コードレビューコマンド定義
│   └── pr-description-reviewer.md  # PR記載レビューコマンド定義
├── README.md
└── LICENSE
```

---

## 🎯 レビュー観点

- **機能性**: 実装が要件を満たしているか
- **可読性**: コードが理解しやすいか、命名は適切か
- **保守性**: 将来の変更に対して柔軟性があるか
- **パフォーマンス**: 効率的な実装になっているか
- **セキュリティ**: セキュリティリスクはないか
- **テスト**: 適切なテストが含まれているか
- **ドキュメント**: 必要な文書化がされているか

---

## 📄 ライセンス

MIT License
