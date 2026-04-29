# oc-install — single-command reproducible install for sst/opencode (Bebond wiring)

Fresh Linux Mint / Ubuntu → ready in ~10 min.

## What it installs

| Component | Destination | Purpose |
|-----------|-------------|---------|
| sst/opencode binary | `~/.opencode/bin/opencode` | The OSS Go TUI/CLI |
| Provider env files | `~/.env.openrouter`, `.env.huggingface`, `.env.nvidia` | API keys |
| opencode.json | `~/.config/opencode/opencode.json` | 3 providers, 6 MCPs, permissions |
| AGENTS.md | `~/.config/opencode/AGENTS.md` | Work rules (copied from existing CLAUDE.md) |
| Memory symlink | `~/.config/opencode/memory` → `~/.claude/projects/-home-alexrollin/memory` | Flat memory files |
| MemPalace | `pip install mempalace` | 10K-drawer local memory store |
| oc-real | `~/.local/bin/oc-real` | Launcher: MemPalace wake-up + SK nutshell + heartbeat |
| oc-overnight | `~/.local/bin/oc-overnight` | Autonomous BBT ticket queue runner |
| mp | `~/.local/bin/mp` | MemPalace search shortcut |
| mount-eed | `~/.local/bin/mount-eed` | gocryptfs vault mounter |
| Desktop launcher | `~/.local/share/applications/OpenCode.desktop` | Click-to-launch |

## 6 MCP servers

| Name | URL | Purpose |
|------|-----|---------|
| bbtracker | `mcp.bebond.net/mcp` | BBT issues/comments/labels |
| aio | `mcp.bebond.net/aio/mcp` | All-in-one (Resend, SMS, email campaigns) |
| sk | `sk-mcp.bebond.net/mcp` | StoryKeeper beats + nutshell |
| bbdev | `dev.bebond.net/mcp` | BB Dev sandbox (47 tools + codemode) |
| bbdocs | `doc.bebond.net/mcp` | BB Docs + Endash decks |
| inkoop | `inkoop.alex-rollin.workers.dev/mcp` | Mouser electronics sourcing |

## Usage

```bash
# One-liner (from GitHub):
curl -fsSL https://raw.githubusercontent.com/alexrollin/oc-install/main/oc-install | bash

# Or clone and run:
git clone https://github.com/alexrollin/oc-install.git
bash oc-install/oc-install

# Dry run (preview what would be installed):
OC_INSTALL_DRY_RUN=1 bash oc-install

# Force overwrite existing files:
OC_INSTALL_FORCE=1 bash oc-install
```

## Environment variables

| Variable | Required | Description |
|----------|----------|-------------|
| `OPENROUTER_API_KEY` | Yes | OpenRouter API key (prompted if missing) |
| `HF_TOKEN` | No | HuggingFace token |
| `NVIDIA_API_KEY` | No | NVIDIA API key |
| `SK_BEAT_TOKEN` | No | StoryKeeper beat token (default: estate service token) |
| `BBDEV_TOKEN` | No | BB Dev sandbox token (default: Bewonersbond Lab key) |
| `OC_INSTALL_FORCE` | No | Set to `1` to overwrite existing files |
| `OC_INSTALL_DRY_RUN` | No | Set to `1` to preview without writing |

## Idempotent

Safe to re-run. Existing files are skipped unless `OC_INSTALL_FORCE=1`.

## Related

- BEB-691 — this ticket
- BEB-675 — worker-harness (server-side)
- BEB-665 — OC login
- BEB-274 — mempalace setup (done)
- BEB-462 — heartbeat rule
