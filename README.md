# todo-shelf はモノレポへ移行しました

このリポジトリは **2026-08-01 に [nyshk97/todo-app](https://github.com/nyshk97/todo-app) へ統合**され、
アーカイブ（読み取り専用）になりました。**開発は todo-app 側で続いています。**

## 移行先

| このリポジトリ | 移行後 |
|---|---|
| `apps/api/` | [`apps/shelf/api/`](https://github.com/nyshk97/todo-app/tree/main/apps/shelf/api) |
| `apps/ios/` | [`apps/shelf/ios/`](https://github.com/nyshk97/todo-app/tree/main/apps/shelf/ios) |
| `apps/web/` | [`apps/shelf/web/`](https://github.com/nyshk97/todo-app/tree/main/apps/shelf/web) |
| `packages/shared/` | [`packages/shelf-shared/`](https://github.com/nyshk97/todo-app/tree/main/packages/shelf-shared) |
| `docs/` | [`docs/shelf/`](https://github.com/nyshk97/todo-app/tree/main/docs/shelf) |
| `scripts/migrate-from-todoist.ts` | `scripts/shelf/migrate-from-todoist.ts` |

## なぜ統合したか

todo-shelf と todo-app は API で連携している（shelf から todo へタスクを移動する）。
別リポジトリだと API 契約を変えるたびに両方へペアのコミットが必要で、
実際に冪等キー対応では todo-app `663ec38` と todo-shelf `c30a3d4` を別々に作る必要があった。
統合後は**1コミットで両側を直せる**。

## 履歴について

このリポジトリの全 55 コミットは履歴ごと todo-app へ取り込まれている（統合コミットは todo-app の `ea34a1b`）。
取り込み時に `git filter-repo` でパスを書き換えたため、**コミット SHA は振り直されている**。

このリポジトリの SHA（例: `cd97f92`）は todo-app には存在しない。対応表を用意してあるので、
移行後の SHA を知りたいときは以下で引く。

```bash
# todo-app 側で実行
grep '^cd97f92' docs/shelf/migration-commit-map.txt
```

このリポジトリ自体は削除せずアーカイブしてあるので、ここの SHA を指す既存の URL は引き続き解決できる。

## 手元の clone を移行する

```bash
git clone git@github.com:nyshk97/todo-app.git
cd todo-app
bash scripts/check-setup.sh   # git 管理外の設定ファイルの過不足を確認
```

統合前から todo-app の clone を持っていた場合は、git 管理外のファイルが旧パスに残っているため:

```bash
git pull origin main
bash scripts/migrate-local-secrets.sh /path/to/todo-shelf
```
