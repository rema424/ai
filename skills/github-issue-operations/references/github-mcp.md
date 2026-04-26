# GitHub MCP

## 結論

GitHub 公式の MCP Server がある。Issue 操作を構造化できるため、`gh api` より安全に扱える場面が多い。

向いている操作:

- issue 作成
- issue 読み取り
- label 参照と更新
- sub-issue 操作
- issue 検索

## Codex での候補構成

`~/.codex/config.toml` に MCP server を追加する。

```toml
[mcp_servers.github]
command = "docker"
args = ["run", "-i", "--rm", "-e", "GITHUB_PERSONAL_ACCESS_TOKEN", "-e", "GITHUB_TOOLSETS", "ghcr.io/github/github-mcp-server"]

[mcp_servers.github.env]
GITHUB_PERSONAL_ACCESS_TOKEN = "YOUR_TOKEN"
GITHUB_TOOLSETS = "issues"
```

まずは `issues` のみで始め、必要なら `repos` や `pull_requests` を足す。

## 運用メモ

- 書き込みを伴うため、PAT scope は最小限にする
- まず read-heavy な運用で導入確認し、その後 write を許可する
- 既存の `gh` Skill と競合させず、MCP があれば MCP、足りない機能だけ `gh` にフォールバックする
