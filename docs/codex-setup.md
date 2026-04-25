# Codex セットアップ手順

この手順は、freee-mcp を Codex Desktop から使うための基本的な準備です。
ここでは、実在するコマンドと、一般的な導入手順だけを案内します。

## 必要なもの

- Codex Desktop アプリ
- Node.js
- Bun
- Git
- freee の利用アカウント
- freee アプリの Client ID / Client Secret

このリポジトリは `packageManager` として `bun@1.3.10` を使っています。

## セットアップ手順

1. リポジトリを clone する
2. リポジトリ直下で依存関係を入れる

```bash
bun install
```

3. freee のアプリを作成し、コールバック URL を設定する

- 例: `http://127.0.0.1:54321/callback`

4. `npx freee-mcp configure` を実行する

```bash
npx freee-mcp configure
```

5. 画面の案内に従って OAuth 認証を行う
6. 事業所を選択する
7. Codex Desktop の MCP 設定に freee-mcp を追加する
8. Codex Desktop から接続確認をする

設定例は [docs/codex-mcp-config-example.md](./codex-mcp-config-example.md) を参照してください。

freee サインを使う場合は、別途次を実行します。

```bash
npx freee-sign-mcp configure
```

## 最初に試す確認コマンド

接続後は、まず読み取りだけで次を確認します。

- 認証状態確認
  - `freee_auth_status`
- 現在のユーザー確認
  - `freee_current_user`
- 事業所一覧取得
  - `freee_list_companies`
- 現在の事業所確認
  - `freee_get_current_company`

## 追加の確認

開発中の MCP サーバーを起動する場合は次を使います。

```bash
bun run dev
```

動作確認やデバッグには、次も使えます。

```bash
bun run inspector
```

必要に応じて、配布前の静的確認も実行します。

```bash
bun run build
bun run typecheck
bun run lint
bun run test:run
```

まとめて確認したいときは、次も使えます。

```bash
bun run check
```

## うまくいかないとき

- `bun install` の後に起動できない
  - `bun run build` をやり直します

- 認証画面が終わらない
  - `npx freee-mcp configure` を再実行して、ブラウザ側の手続きを最後まで完了します

- Codex Desktop が接続先を見つけない
  - 設定ファイルと起動コマンドを見直し、Codex Desktop を再起動します

- 事業所が出てこない
  - `freee_list_companies` と `freee_get_current_company` で状況を確認します
