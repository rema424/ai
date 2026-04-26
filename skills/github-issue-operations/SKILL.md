---
name: github-issue-operations
description: "Use when operating GitHub Issues across repositories with `gh` or a GitHub MCP server. Covers issue create/edit/view/close, label inspection, bulk issue workflows, sub-issue linking, `gh api` payload typing, issue number vs REST id, auth checks, and restart-safe recovery after partial failures."
license: MIT
---

# GitHub Issue Operations

GitHub Issue 運用は、可能なら GitHub MCP を優先し、未設定または不足機能がある場合は `gh` CLI を使う。

## Preflight

1. 認証を確認する: `gh auth status`
2. 対象 repo を確定する。書き込み系は `-R OWNER/REPO` を明示する
3. 一括処理の前に、親 Issue、子 Issue、label の存在を読む
4. 大量更新は本番一括で始めず、まず 1-3 件で検証する

## 標準コマンド

- 作成: `gh issue create -R OWNER/REPO --title ... --body-file ...`
- 編集: `gh issue edit -R OWNER/REPO NUMBER --add-label ...`
- 閲覧: `gh issue view -R OWNER/REPO NUMBER --json id,number,title,labels,state,url`
- クローズ: `gh issue close -R OWNER/REPO NUMBER --reason completed`
- label 一覧: `gh label list -R OWNER/REPO --json name,description,color`

本文が長い場合は `--body-file` を使う。shell quoting を減らし、再実行しやすくする。

## `gh api` の原則

- `gh api` の endpoint は `repos/{owner}/{repo}/...` 形式を基本にする
- `{owner}` `{repo}` の placeholder は現在 repo か `GH_REPO` から補完される
- `-f` は文字列専用
- `-F` は整数、真偽値、`null`、placeholder、`@file` を型付きで送れる
- 数値や boolean を送る API は、まず `-F` を検討する

## Sub-issue の注意点

- `sub_issue_id` は issue number ではなく REST `id`
- 親子付け前に親 Issue と子 Issue を読み、既存の親子関係を確認する
- 既に親子付け済みの再追加で `422` になり得る。再実行時は失敗ではなく既存状態を確認してから次へ進む
- 子の親を差し替える必要がある場合だけ `replace_parent=true` を使う

## 一括処理の原則

- 長大なワンライナーを避ける
- 再実行単位を小さく保つ
- 中間結果は TSV / JSON で残す
- 各段階の直後に代表サンプルを確認する

## 推奨手順

1. 認証確認
2. 対象取得
3. 小さな検証バッチ
4. 本処理
5. 代表確認
6. 未完了分だけ再開

## 失敗時の再開

- 作成済み Issue は `gh issue list` / `gh issue view` で突き合わせる
- parent-child 紐付けは親ごとに現状態を読んで差分だけ再送する
- label 付与は対象 Issue の label 一覧を読み、未付与だけ追加する

詳しいレシピと MCP 設定例は `references/templates.md` と `references/github-mcp.md` を読む。
