# MESMO — Agent Instructions

## Agent skills

### Issue tracker

Issues live as GitHub issues in the fork `MingzhiZhang/mesmo` — always pass `--repo MingzhiZhang/mesmo` to `gh`, never write to `upstream` (`mesmo-dev/mesmo`). See `docs/agents/issue-tracker.md`.

### Triage labels

The five canonical roles, using their default names (`needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, `wontfix`). See `docs/agents/triage-labels.md`.

### Domain docs

Single-context: one `CONTEXT.md` at the root plus `docs/adr/`. See `docs/agents/domain.md`.
