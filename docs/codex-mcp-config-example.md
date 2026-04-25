# Codex MCP 設定例

このファイルは、Codex Desktop に freee-mcp をつなぐときの例です。
実際の設定画面や JSON の形は、Codex Desktop の版や導入方法で変わることがあります。
ここにある内容は、最終形を保証するものではありません。

## 例

```json
{
  "mcpServers": {
    "freee-mcp": {
      "command": "bun",
      "args": ["run", "src/index.ts"],
      "cwd": "/Users/ryukouokumura/Desktop/freee-mcp-codex"
    }
  }
}
```

## 補足

- ローカル開発では、リポジトリの実体をそのまま使う例です
- すでに `freee-mcp` をインストールしている環境では、別の `command` に置き換えることがあります
- 実際の設定では、Codex Desktop が案内する保存先や編集方法に従ってください
- 読み取り専用で始め、書き込み系は人間確認を挟んでください

