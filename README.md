# ai

Agent tooling shared by rema424.

## Skills

This repository currently publishes these Codex skills:

- `github-issue-operations`
- `hi-fi-spike-decision`
- `hi-fi-spike-handoff`
- `spiral-autonomy`

## Install

Install skills interactively with GitHub CLI:

```sh
gh skill install rema424/ai --agent codex --scope user
```

This opens an interactive selector for the skills in this repository.
Use `--agent codex` to install for Codex, and `--scope user` to make the
installed skills available across repositories.

## APM

This repository can also be packed as an APM plugin:

```sh
apm pack --format plugin
```
