# git-prompts

**Git-native versioning & review for AI prompts — prompts travel with the code they help create.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python](https://img.shields.io/badge/python-3.9%2B-blue)](https://www.python.org/)
[![GitHub stars](https://img.shields.io/github/stars/nirmorgo/git-prompts?style=social)](https://github.com/nirmorgo/git-prompts)

In 2026, AI writes a huge chunk of your code — but prompts are still treated like throwaway notes.  
**git-prompts** changes that: it automatically captures the exact prompts and generation metadata (model, temperature, output hash, etc.) **inside your Git commits**, only when code is AI-generated. Reviewers see both the code **and** the instructions that produced it — right in Git diffs and PRs.

No separate tools. No parallel workflows. Just better, more transparent code reviews.

## ✨ Why git-prompts?

- **Seamless Git integration** — hooks capture prompts during normal `git commit` / `git push`
- **Prompts linked to code** — sidecar files in `.prompts/` + Git trailers/notes for association
- **Reviewer-first design** — prompts appear inline in PRs (GitHub/GitLab) so reviewers can critique instructions, not just output
- **Zero friction** — opt-in per repo, lightweight, no daemon/server needed
- **Audit & provenance** — trace bugs, regressions, or policy violations back to the exact prompt

Perfect for teams using Cursor, Claude Code, Copilot, Continue.dev, Grok, or any AI coding assistant.

## 🚀 Quick Start

1. Install (coming soon — for now clone & run from source)

        git clone https://github.com/nirmorgo/git-prompts.git
        cd git-prompts
        pip install -e .

2. Initialize in your project

        git prompt init

   This adds Git hooks and creates `.prompts/.gitignore`-friendly structure.

3. Generate code with AI (e.g., in VS Code / Cursor)

   When your IDE saves AI-generated code, it should tag it (future: auto-detect or IDE plugin).

   Commit with flag for now:

        git commit -m "Add user auth endpoint" --ai-prompt

   → Automatically stages `.prompts/auth.py.prompt.md` and `.prompts/auth.py.prompt.json`

4. Push & create PR

   Reviewers see diffs like:

        # auth.py
        +def login(...): ...

        Associated prompt:
        "Write secure FastAPI login endpoint with JWT, rate limiting, and OAuth2 support. Handle common errors gracefully."
        Metadata: Grok-4 • temp=0.4 • max_tokens=2000 • generated: 2026-02-20T22:15Z

## 📂 How It Works (MVP)

- `.prompts/<filename>.prompt.md` — the raw prompt text (Markdown-friendly)
- `.prompts/<filename>.prompt.json` — metadata:

        {
          "model": "grok-4",
          "temperature": 0.7,
          "max_tokens": 4096,
          "output_hash": "sha256:abc123...",
          "session_id": "claude-abc-123",
          "timestamp": "2026-02-20T22:43:00Z",
          "linked_file": "src/auth.py"
        }

- Git hooks (pre-commit, post-commit) detect AI-generated files (via flag, comment pattern, or future IDE signal)
- Git trailers (`Prompt-File: .prompts/...`) link commits to prompts without bloating history

## 🛠️ Current Status (Feb 2026)

- Repo just born! MVP hooks + CLI skeleton coming in days
- Planned v0.1 (next 1-2 weeks):
  - Basic hooks & CLI (`git prompt init`, `git prompt status`)
  - Manual flag support (`--ai`)
  - Simple diff rendering instructions for GitHub

## 📈 Roadmap

- v0.2: Auto-detection heuristics + VS Code extension prototype
- v0.3: GitHub Action for prompt linting / auto-testing in CI
- v0.4: Semantic diff for prompts + inline PR rendering (browser ext or GitHub App)
- Future: Local model replay, prompt A/B metrics, team collaboration dashboard (if demand)

## 🤝 Contributing

Love the idea? Jump in!

1. ⭐ Star the repo
2. Check [open issues](https://github.com/nirmorgo/git-prompts/issues)
3. Fork → branch → PR
4. Good first issues will be labeled soon

See [CONTRIBUTING.md](CONTRIBUTING.md) (coming soon) for setup & style.

Discussions, feature requests, bug reports — all welcome in Issues.

Built with ❤️ by [@nirmorgo](https://github.com/nirmorgo)

MIT Licensed — free to use, fork, modify, sell your soul with, etc.
