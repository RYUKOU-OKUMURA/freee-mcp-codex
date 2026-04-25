# 検証計画

この計画は、実装後に最低限確認する手順です。
ここに書くコマンドは、`package.json` にあるものか、一般的なインストール手順だけに限定します。

## 1. 依存関係の導入

```bash
bun install
```

依存関係が正しく入ることを確認します。

## 2. 型の確認

```bash
bun run typecheck
```

TypeScript の型エラーがないことを確認します。

## 3. リント確認

```bash
bun run lint
```

コードの書き方に大きな問題がないかを確認します。

## 4. 総合チェック

```bash
bun run check
```

整形とリントの両方をまとめて確認します。

## 5. テスト実行

```bash
bun run test:run
```

テストが通ることを確認します。

## 6. ビルド確認

```bash
bun run build
```

配布用のビルドが最後まで通ることを確認します。

## 7. 初回接続確認

```bash
npx freee-mcp configure
```

認証情報の設定、OAuth 認証、事業所選択まで通ることを確認します。

## 8. Codex MCP 接続確認

- Codex Desktop から freee-mcp の MCP サーバーが見えるか確認する
- 認証状態確認を行う
  - `freee_auth_status`
- 現在のユーザー確認を行う
  - `freee_current_user`
- 事業所一覧取得を行う
  - `freee_list_companies`
- 現在の事業所確認を行う
  - `freee_get_current_company`

## 9. 読み取り系 API 確認

- `GET` 系の取得だけで確認する
- 事業所、ユーザー、取引、取引先、勘定科目、請求書の一覧を確認する
- 結果は表で残す
- 曖昧な点は `要確認` に分ける

## 10. 書き込み系 API の扱い

- `POST` `PUT` `PATCH` `DELETE` は、テストデータまたは明示確認後のみ実行する
- 実データに対する削除は原則使わない
- 実行前に、API パス、HTTP メソッド、送信内容、影響範囲を日本語で説明する

## 11. 確認結果の記録方法

- 実行したコマンド
- 成否
- 失敗した場合のエラーメッセージ
- 参照した事業所と対象期間
- 人が確認したかどうか

## 12. 確認の見方

- まず `bun install` で依存関係を揃える
- 次に `typecheck` と `lint` で静的な問題を止める
- その後に `test:run` で挙動を確認する
- 最後に `build` と `inspector` で配布前の見え方を確認する
