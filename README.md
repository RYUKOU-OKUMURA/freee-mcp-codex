# freee-mcp-codex

freee-mcp を Codex Desktop から安全に導入、接続、検証、運用するための非公式スターターキットです。

このリポジトリは freee-mcp をベースにしていますが、フリー株式会社の公式提供物ではありません。同社による承認、保証、サポートを意味するものでもありません。

まずは読み取り専用で始め、登録、更新、削除は必ず人間の確認を挟む前提で使います。税務判断、会計判断、顧問先への説明の最終責任は人間にあります。

[![npm version](https://badge.fury.io/js/freee-mcp.svg)](https://www.npmjs.com/package/freee-mcp)

## このリポジトリの目的

- Codex Desktop から freee-mcp を使うための導入手順をまとめる
- 税理士事務所や freee 利用者が読み取り専用から安全に試せるようにする
- MCP 設定例、AGENTS.md、業務プロンプト、安全運用ルールを用意する
- 公式提供物と誤認されない形で、freee-mcp の Codex 利用を補助する

## 最初に読むもの

- [docs/codex-setup.md](./docs/codex-setup.md)
  - セットアップ手順です。
- [docs/codex-mcp-config-example.md](./docs/codex-mcp-config-example.md)
  - Codex 向け MCP 設定例です。
- [docs/safety-policy-for-tax-accountants.md](./docs/safety-policy-for-tax-accountants.md)
  - 税理士事務所向けの安全運用方針です。
- [prompts/00-read-only-check.md](./prompts/00-read-only-check.md)
  - 初回の読み取り専用チェック用プロンプトです。

## Codex で最初にできること

最初は次のような読み取り系だけを試してください。

- 事業所一覧の取得
- 現在の事業所確認
- ユーザー情報確認
- 取引一覧取得
- 取引先一覧取得
- 勘定科目一覧取得
- 請求書一覧取得

書き込みが必要な場合も、まず下書き案を表で確認します。`POST`、`PUT`、`PATCH`、`DELETE` は、人間が明示的に許可するまで実行しない運用にしてください。

## セットアップ概要

1. 依存関係を入れる

```bash
bun install
```

2. freee-mcp の初期設定を行う

```bash
npx freee-mcp configure
```

3. Codex Desktop の MCP 設定に freee-mcp を追加する

設定例は [docs/codex-mcp-config-example.md](./docs/codex-mcp-config-example.md) を参照してください。

4. 読み取り系の接続確認から始める

- `freee_auth_status`
- `freee_current_user`
- `freee_list_companies`
- `freee_get_current_company`

## 業務プロンプト

税理士事務所や事務所スタッフが Codex に貼り付けて使えるプロンプトを用意しています。

- [prompts/00-read-only-check.md](./prompts/00-read-only-check.md)
- [prompts/01-monthly-review.md](./prompts/01-monthly-review.md)
- [prompts/02-invoice-draft.md](./prompts/02-invoice-draft.md)
- [prompts/03-expense-review.md](./prompts/03-expense-review.md)
- [prompts/04-duplicate-check.md](./prompts/04-duplicate-check.md)
- [prompts/05-client-report-draft.md](./prompts/05-client-report-draft.md)

共通ルールは、読み取り優先、表で整理、要確認を分離、書き込み前の人間確認です。

## freee-mcp の主な機能

このスターターキットは、元の freee-mcp が提供する MCP サーバーと Agent Skills を利用します。

- 会計 API
- 人事労務 API
- 請求書 API
- 工数管理 API
- 販売 API
- freee サイン API

代表的な MCP ツールは次の通りです。

| ツール | 説明 |
| --- | --- |
| `freee_auth_status` | 認証状態の確認 |
| `freee_current_user` | 現在のユーザー情報 |
| `freee_list_companies` | 事業所一覧 |
| `freee_get_current_company` | 現在の事業所 |
| `freee_api_get` | データ取得 |
| `freee_api_post` | 新規作成 |
| `freee_api_put` | 更新 |
| `freee_api_patch` | 部分更新 |
| `freee_api_delete` | 削除 |
| `freee_api_list_paths` | エンドポイント一覧 |

削除系 API は原則使わないでください。

## Claude Code との違い

元の freee-mcp には Claude Desktop や Claude Code Plugin 向けの導線があります。このリポジトリでは、Codex Desktop で使うために、MCP 設定、Skills、AGENTS.md、プロンプト集、安全運用ドキュメントを組み合わせる形に整理しています。

詳しくは [docs/claude-to-codex-notes.md](./docs/claude-to-codex-notes.md) を参照してください。

## 検証

検証手順は [docs/verification-plan.md](./docs/verification-plan.md) にまとめています。

主な確認コマンドは次の通りです。

```bash
bun run typecheck
bun run lint
bun run test:run
bun run build
```

実 API 接続や書き込み系 API の確認は、テストデータまたは人間の明示確認後に限定してください。

## 開発者向け

```bash
git clone https://github.com/RYUKOU-OKUMURA/freee-mcp-codex.git
cd freee-mcp-codex
bun install

bun run dev
bun run build
bun run typecheck
bun run lint
bun run test:run
```

内部構造や既存の開発ガイドは [CLAUDE.md](./CLAUDE.md) に残っています。ただし Codex で freee データを扱うときの行動ルールは [AGENTS.md](./AGENTS.md) を優先してください。

## ライセンスと商標

元の freee-mcp は Apache License 2.0 で提供されています。詳細は [LICENSE](./LICENSE) を確認してください。

元になっている公式リポジトリはこちらです。

- [freee/freee-mcp](https://github.com/freee/freee-mcp)

freee および関連するサービス名は、フリー株式会社の商標または登録商標です。Codex、OpenAI、Claude などの名称も、それぞれの権利者に帰属します。

## Contributors

元リポジトリ由来の Contributors です。

<!-- CONTRIBUTORS-START -->
<a href="https://github.com/him0"><img src="https://github.com/him0.png" width="40" height="40" alt="@him0"></a>
<a href="https://github.com/dais0n"><img src="https://github.com/dais0n.png" width="40" height="40" alt="@dais0n"></a>
<a href="https://github.com/HikaruEgashira"><img src="https://github.com/HikaruEgashira.png" width="40" height="40" alt="@HikaruEgashira"></a>
<a href="https://github.com/nakanoasaservice"><img src="https://github.com/nakanoasaservice.png" width="40" height="40" alt="@nakanoasaservice"></a>
<a href="https://github.com/tackeyy"><img src="https://github.com/tackeyy.png" width="40" height="40" alt="@tackeyy"></a>
<a href="https://github.com/worldscandy"><img src="https://github.com/worldscandy.png" width="40" height="40" alt="@worldscandy"></a>
<a href="https://github.com/akhr77"><img src="https://github.com/akhr77.png" width="40" height="40" alt="@akhr77"></a>
<a href="https://github.com/trpfrog"><img src="https://github.com/trpfrog.png" width="40" height="40" alt="@trpfrog"></a>
<a href="https://github.com/hoshinotsuyoshi"><img src="https://github.com/hoshinotsuyoshi.png" width="40" height="40" alt="@hoshinotsuyoshi"></a>
<a href="https://github.com/JeongJaeSoon"><img src="https://github.com/JeongJaeSoon.png" width="40" height="40" alt="@JeongJaeSoon"></a>
<a href="https://github.com/norimura114"><img src="https://github.com/norimura114.png" width="40" height="40" alt="@norimura114"></a>
<a href="https://github.com/akiras-ssrd"><img src="https://github.com/akiras-ssrd.png" width="40" height="40" alt="@akiras-ssrd"></a>
<a href="https://github.com/inoue2002"><img src="https://github.com/inoue2002.png" width="40" height="40" alt="@inoue2002"></a>
<a href="https://github.com/jacknocode"><img src="https://github.com/jacknocode.png" width="40" height="40" alt="@jacknocode"></a>
<a href="https://github.com/tnj"><img src="https://github.com/tnj.png" width="40" height="40" alt="@tnj"></a>
<a href="https://github.com/jaxx2104"><img src="https://github.com/jaxx2104.png" width="40" height="40" alt="@jaxx2104"></a>
<a href="https://github.com/kbyk004"><img src="https://github.com/kbyk004.png" width="40" height="40" alt="@kbyk004"></a>
<a href="https://github.com/k4200"><img src="https://github.com/k4200.png" width="40" height="40" alt="@k4200"></a>
<a href="https://github.com/fukumayuta"><img src="https://github.com/fukumayuta.png" width="40" height="40" alt="@fukumayuta"></a>
<a href="https://github.com/kenchan"><img src="https://github.com/kenchan.png" width="40" height="40" alt="@kenchan"></a>
<a href="https://github.com/EijiSugiura"><img src="https://github.com/EijiSugiura.png" width="40" height="40" alt="@EijiSugiura"></a>
<a href="https://github.com/ryuuuuma"><img src="https://github.com/ryuuuuma.png" width="40" height="40" alt="@ryuuuuma"></a>
<a href="https://github.com/toyamagu-2021"><img src="https://github.com/toyamagu-2021.png" width="40" height="40" alt="@toyamagu-2021"></a>
<a href="https://github.com/YasuakiOmokawa"><img src="https://github.com/YasuakiOmokawa.png" width="40" height="40" alt="@YasuakiOmokawa"></a>
<a href="https://github.com/Kitamura777"><img src="https://github.com/Kitamura777.png" width="40" height="40" alt="@Kitamura777"></a>
<a href="https://github.com/yuyohi"><img src="https://github.com/yuyohi.png" width="40" height="40" alt="@yuyohi"></a>
<!-- CONTRIBUTORS-END -->

## 関連リンク

- [freee API ドキュメント](https://developer.freee.co.jp/docs)
- [Model Context Protocol](https://modelcontextprotocol.io)
- [freee/freee-mcp](https://github.com/freee/freee-mcp)
- [freee-mcp npm package](https://www.npmjs.com/package/freee-mcp)
