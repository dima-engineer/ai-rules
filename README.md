# ai-rules

Shared AI agent skills for OpenCode, Claude Code, and Cursor.

| Skill | Purpose |
|---|---|
| `create-task` | Turn a high-level description into a backlog task and save it to the project's task system. |
| `work-on-task` | Structured flow for implementing a task: read, explore, clarify, plan, implement, report. |
| `open-pr` | Run checks, commit, enforce the PR size limit, and open a PR after approval. |
| `fix-pr` | Fix failing checks and unresolved review comments on a PR. |
| `decompose-pr` | Split an oversized branch into stacked branches. Only used when explicitly asked (e.g. by `open-pr`). |

Each harness has its own copy, adapted to its tools:

| Folder | Harness |
|---|---|
| `opencode/skills/` | OpenCode (source of truth) |
| `claude/skills/` | Claude Code |
| `cursor/skills/` | Cursor |

When you change a skill, change it in `opencode/skills/` first, then port the change to the other two.

Clone the repo first:

```bash
git clone git@github.com:dima-engineer/ai-rules.git ~/Projects/ai-rules
```

To update, `git pull` in the repo.

## OpenCode

1. Add the skills folder to the `skills` array in `~/.config/opencode/opencode.json`:

   ```jsonc
   {
     "$schema": "https://opencode.ai/config.json",
     "skills": ["~/Projects/ai-rules/opencode/skills"]
   }
   ```

   OpenCode reloads config on save. Skills added to the repo later are picked up automatically.

2. Check that the skills are loaded:

   ```bash
   opencode api get /api/skill > /tmp/skills.json
   python3 -c "import json; [print(s['id'], s['path']) for s in json.load(open('/tmp/skills.json'))['data'] if 'ai-rules' in s['path']]"
   ```

Skills from the `skills` config entry take precedence over skills with the same ID in `~/.config/opencode/skills`, `~/.claude/skills`, and `~/.agents/skills`.

## Claude Code

Symlink each skill into `~/.claude/skills/`:

```bash
mkdir -p ~/.claude/skills
for s in create-task work-on-task open-pr fix-pr decompose-pr; do
  ln -sfn ~/Projects/ai-rules/claude/skills/$s ~/.claude/skills/$s
done
```

Run them with `/open-pr`, `/work-on-task BL-012`, etc., or let Claude pick them up from context. If a running session doesn't see them, run `/reload-skills`.

## Cursor

Symlink each skill into `~/.cursor/skills/`:

```bash
mkdir -p ~/.cursor/skills
for s in create-task work-on-task open-pr fix-pr decompose-pr; do
  ln -sfn ~/Projects/ai-rules/cursor/skills/$s ~/.cursor/skills/$s
done
```

Run them with `/open-pr` etc., or let the agent pick them up from context. `decompose-pr` has `disable-model-invocation: true`; `open-pr` hands it to a subagent by file path, so keep both installed side by side.

Cursor also reads `~/.claude/skills/`. If you install the Claude Code skills too, Cursor will see each skill twice.

## PR template for `open-pr` (optional)

`open-pr` follows a `PR_TEMPLATE.md` placed next to its `SKILL.md`. The file is git-ignored (`*/skills/*/PR_TEMPLATE.md`), so each machine can have its own. It can contain the template itself or say where to get it:

```markdown
# PR template

Fetch the PR template fresh for every PR:

https://raw.githubusercontent.com/<org>/.github/main/PULL_REQUEST_TEMPLATE.md

Keep the description short: what the PR does and why. No file-by-file change lists.
```

Write it once in `opencode/skills/open-pr/` and link it into the other harnesses:

```bash
cd ~/Projects/ai-rules
ln -sfn ../../../opencode/skills/open-pr/PR_TEMPLATE.md claude/skills/open-pr/PR_TEMPLATE.md
ln -sfn ../../../opencode/skills/open-pr/PR_TEMPLATE.md cursor/skills/open-pr/PR_TEMPLATE.md
```

Without it, `open-pr` writes a free-form description.
