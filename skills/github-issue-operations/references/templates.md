# Templates

## Issue 一括作成

1. 対象定義を `JSON` または `TSV` にまとめる
2. まず 1-3 件だけ `gh issue create -R OWNER/REPO --title ... --body-file ...` で作成する
3. `gh issue view` で title, body, labels を確認する
4. 問題なければ残りを同じ入力定義から処理する
5. 作成結果は `title -> number,id,url` の対応表として保存する

推奨:

```bash
gh issue create -R OWNER/REPO \
  --title "$TITLE" \
  --body-file "$BODY_FILE" \
  --label "$LABEL_A" \
  --label "$LABEL_B"
```

## Sub-issue 紐付け

事前確認:

```bash
gh issue view -R OWNER/REPO "$PARENT_NUMBER" --json id,number,title,url
gh issue view -R OWNER/REPO "$CHILD_NUMBER" --json id,number,title,url
```

子の REST `id` を取り、親へ追加する:

```bash
gh api \
  -X POST \
  "repos/OWNER/REPO/issues/$PARENT_NUMBER/sub_issues" \
  -F "sub_issue_id=$CHILD_REST_ID"
```

再実行時:

1. 親 Issue の sub-issue 一覧を先に読む
2. 既存なら skip する
3. `422` は即停止せず、既存親子関係を確認して分類する

## Label 一括付与

1. `gh label list -R OWNER/REPO --json name` で存在確認
2. 代表 2-3 件へ `gh issue edit --add-label` を試す
3. 問題なければ残りへ展開する
4. 最後に代表数件を `gh issue view --json labels` で確認する

推奨:

```bash
gh issue edit -R OWNER/REPO "$NUMBER" \
  --add-label "$LABEL_A" \
  --add-label "$LABEL_B"
```

## 途中失敗時の再開

1. 入力一覧と完了一覧を別に持つ
2. 完了一覧には `number` と `id` の両方を保存する
3. 再開時は API エラーを信頼しすぎず、現状態を読んで差分だけ再送する
4. parent-child は親単位、label は issue 単位で再開する

## 運用ルール

- まず小分けで検証する
- 失敗前提で途中状態を保存する
- shell quoting が増える処理は `--body-file` や入力ファイルに逃がす
- repo 依存の暗黙値を減らすため、書き込み系は `-R OWNER/REPO` を明示する
