# Setup

## spiral-autonomy Subagent Authorization

Codex can load skills from this repository, but subagent authorization is controlled by Codex runtime configuration, not by a skill or plugin alone. To make `$spiral-autonomy` count as explicit authorization for subagents, add `developer_instructions` to Codex config.

User-level config:

```text
~/.codex/config.toml
```

Project-level config:

```text
.codex/config.toml
```

Project-level config is loaded only for trusted projects.

Recommended user-level configuration. Place this top-level key before any TOML table header such as `[projects "..."]` or `[tui.model_availability_nux]`:

```toml
developer_instructions = """
The user's invocation of $spiral-autonomy counts as explicit authorization for subagents, delegation, and parallel agent work.

When spiral-autonomy is active, use the maximum useful parallelism available by default.
Keep subagents continuously supplied with bounded concrete tasks until the mission objective is achieved or a real stop condition is reached.

Do not use subagents as generic search engines.
Assign high-load research, design, implementation, testing, review, validation, or risk-analysis outputs.
Keep the critical path local, avoid duplicate work, and give implementation workers disjoint write scopes.
"""
```

After changing Codex config, start a new Codex session. Existing sessions do not reload developer instructions.

To install the recommended user-level config automatically, run:

```sh
scripts/install-config
```

The script installs the block as a top-level key before any TOML table header. If an older run placed this same block under a table, the script repairs it. If `developer_instructions` already exists with different content, the script leaves the file unchanged and asks you to merge manually.
