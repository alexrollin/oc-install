# oc-install repo

Single-command reproducible install for sst/opencode on Alex's laptop (Bebond wiring).

## Key files
- `oc-install` — the main install script (idempotent, ~400 lines)

## Rules
- Never bake real API keys into committed source — tokens use env-var defaults or prompts
- Never push to main — branch + PR + squash-merge
- Never Docker, never Anthropic API, never gh issue create
