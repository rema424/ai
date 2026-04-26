---
name: hi-fi-spike-handoff
description: Use after a branch has been reclassified as a Hi-Fi Spike. Extracts lessons, test intent, failure patterns, design constraints, minimal whiteboard design, and creates a handoff document for autonomous clean-room production implementation from a base branch.
license: MIT
---

# Hi-Fi Spike Handoff

Use this skill after the decision to treat the current branch as a Hi-Fi Spike has already been made.

The goal is not to preserve or port spike implementation code. The goal is to preserve lessons so the next session can implement production code from a clean base as autonomously as possible, including tests and requirements verification.

## Hard Rules

Discard:

- code newly written in the spike
- spike-created file names, function names, and implementation details
- accidental branches, duplicate state, conversions, sync paths, and corrective logic added only to make the spike work

Preserve:

- test intent
- structural lessons about the existing codebase
- failure and regression patterns
- contract, state machine, authoritative source, and invariant decisions
- simplification rules for the clean-room implementation

Existing code names may be mentioned when they are structural findings about the pre-existing codebase. Spike-created names must not be carried into the handoff.

## Workflow

### 0. Confirm Preconditions

State:

- current branch
- base branch for clean-room production implementation
- diff range to discard
- that spike code will not be directly ported

If these cannot be identified, ask before creating the final handoff.

### 1. Reconfirm Requirements

Classify requirements into:

- **現行維持**: behavior and compatibility to keep
- **変更する**: behavior redefined by spike lessons
- **追加要件**: requirements discovered only through implementation or regression
- **非要件**: things not to carry into production

### 2. Describe the Whiteboard-Minimal Design

Ignore the spike implementation shape. Describe the simplest production design that satisfies the requirements:

- essential responsibility
- responsibility boundaries
- authoritative source for state, entities, and progress
- contract / API / type / protocol boundaries
- state machine, valid transitions, invalid intermediate states
- invariants that should be fixed in code or tests
- minimal modules / components / APIs / state
- data flow that avoids duplicate truth
- complexity that can be deleted or avoided

Explain why the design is minimal.

### 3. Extract Test Intent

Use spike tests only as sources of intent. Do not copy their code shape.

Extract lessons at three layers:

- **要件レイヤー**: acceptance / e2e behavior, user-visible outcomes, requirement gaps
- **基本設計レイヤー**: integration boundaries, authoritative source, backend/frontend truth, contract clarity, optimistic UI assumptions
- **詳細設計レイヤー**: algorithms, data structures, boundary cases, errors, invariants

### 4. Extract Lessons

Capture:

- what worked and should influence production design
- what failed and must not be repeated
- the common root of failures, if present
- regression patterns such as "fix A reopened B"
- sources of complexity: branches, state, conversions, synchronization, correction logic, exceptions
- structural findings about existing code
- library, framework, external API, or dependency constraints

Phrase lessons as principles and constraints, not implementation details.

### 5. Define the Production Implementation Plan

State:

- base branch and discarded diff range
- what to fix first: contract, state machine, authoritative source, invariants
- smallest vertical slice to implement first
- slice order and dependencies
- recommended approaches from the spike
- approaches to avoid
- tests to add or update, especially regression tests

Prefer a plan that enables autonomous implementation, testing, and requirements verification in the next session.

## Handoff Template

Produce the final document in this structure:

`````markdown
# Hi-Fi Spike Handoff: {テーマ}

## 1. 背景・目的

## 2. 現在の状況

- 現ブランチ:
- ベースブランチ:
- 捨てる diff の範囲:
- spike 実装を直接移植しない理由:

## 3. 要件

### 3.1 現行維持

### 3.2 変更する

### 3.3 spike で発見した追加要件

### 3.4 非要件

## 4. 白紙設計での最小構成

### 4.1 本質的な責務

### 4.2 authoritative source

### 4.3 契約と状態機械

### 4.4 最小構成案

### 4.5 削れる複雑性

## 5. テストが明らかにした仕様

### 5.1 要件レイヤー

### 5.2 基本設計レイヤー

### 5.3 詳細設計レイヤー

## 6. Spike からの教訓

### 6.1 うまくいったこと

### 6.2 うまくいかなかったこと

### 6.3 失敗の共通根

### 6.4 regression パターン

### 6.5 複雑性の発生源

### 6.6 構造的発見

### 6.7 制約・落とし穴

## 7. 本番実装の方針

### 7.1 起点と範囲

### 7.2 固定する順序

### 7.3 スライス戦略

### 7.4 推奨アプローチ

### 7.5 避けるべきアプローチ

### 7.6 追加すべきテスト観点

## 8. 次セッションへのメッセージ

次セッションでは、この Handoff だけを前提に、可能な限り自律的に本番実装を完了せよ。
spike ブランチの新規実装コードは参照・移植しない。必要な学びはこの文書内に抽象化済みである。

### 8.1 自律実行の目的

1. ベースブランチから白紙で本番実装する
2. 必要なテストを追加・更新する
3. 既存テストと新規テストを実行する
4. 要件充足を Handoff の要件一覧に照らして検証する
5. 未充足・未検証・残リスクを明示する

単にコードを書くことではなく、実装・テスト・要件充足確認まで完了させることをゴールとする。

### 8.2 実行方針

- まず Handoff の要件、白紙設計、固定する順序を読み、実装前に短い作業計画を作る
- 最初に authoritative source、契約、状態機械を固定する
- その後、最小の縦スライスから実装する
- spike 由来の複雑性を再導入しない
- 判断に迷った場合は、より単純で説明しやすい設計を優先する
- 既存の設計・テスト・lint・型チェックの流儀に従う
- 実装後に要件ごとの充足状況をチェックする

### 8.3 自律実行の許可範囲

次セッションでは、以下を自律的に進めてよい。

- 関連コードの調査
- 本番実装
- テスト追加・更新
- lint / typecheck / unit test / integration test / e2e test の実行
- 失敗したテストの原因調査と修正
- 要件充足チェックリストの作成
- 実装内容に必要な最小限の docs / comments 更新

ただし、以下に該当する場合は作業を止めてユーザーに確認する。

- 要件が Handoff と矛盾している
- ベースブランチや捨てる diff の範囲が不明
- destructive な git 操作が必要
- migration / data rewrite / secret / credential に触れる
- 権限拡大が必要
- 同じ種類の failure が 2 回続く
- 実装範囲が Handoff の想定を超えて広がる
- 要件を満たすには設計方針を変更する必要がある

### 8.4 完了条件

- [ ] Handoff の要件が実装に反映されている
- [ ] authoritative source が明確で、truth が複数箇所に分岐していない
- [ ] 契約・状態機械・invariants が実装またはテストで固定されている
- [ ] spike で失敗したアプローチを再導入していない
- [ ] regression パターンを防ぐテストが追加または更新されている
- [ ] 既存テストが通っている
- [ ] 新規テストが通っている
- [ ] lint / typecheck / format など、repo の標準検証が通っている
- [ ] 要件ごとの充足・未充足・未検証が明示されている
- [ ] 残リスクがある場合は、理由と次アクションが明示されている

### 8.5 最終報告の形式

```markdown
## 実装結果

- 実装したこと:
- 変更した主要ファイル:
- 採用した設計:
- 再導入しなかった spike 由来の複雑性:

## 要件充足確認

| 要件 | 状態 | 根拠 |
| --- | --- | --- |
| ... | OK / 未充足 / 未検証 | ... |

## 検証結果

### 実施した検証

- ...

### 未実施の検証

- ...

## 残リスク

- ...

## 次アクション

- ...
```

### 8.6 重要な注意

この Handoff は、次セッションに追加調査だけをさせるための文書ではない。
目的は、可能な範囲で設計判断、実装、テスト、要件充足確認までを自律的に完了することである。

ただし、自律性は無制限ではない。
Handoff の範囲、repo の検証手順、権限上限、停止条件を超える場合は、実装を進めずユーザーに確認する。
`````

## Final Self-Check

Before finalizing the handoff, verify:

- no spike-created file names, function names, or implementation details are included
- lessons are principles, not code details
- common root of failures is explicit
- complexity sources and simplification opportunities are explicit
- authoritative source is explicit
- contract and state machine are fixed early
- production base branch is explicit
- autonomous scope, stop conditions, and completion criteria are explicit
- the next session can start implementation from this document without reading spike code
