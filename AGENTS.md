# Repository Guidelines

本仓库是 [Fei-Away/Codex-Dream-Skin](https://github.com/Fei-Away/Codex-Dream-Skin) 的精简 fork，仅保留 macOS 个人使用所需部分。

## Project Structure

- `macos/` is the product: shell launchers, `scripts/` runtime logic, `assets/` CSS/injection payloads, `menubar/` SwiftBar integration, and `tests/` checks.
- `docs/images/gallery/` holds README preview composites, not theme backgrounds.

## Build, Test, and Development Commands

- `cd macos && npm test`: run shell/JavaScript syntax, payload, configuration round-trip, signature, and doctor checks.
- `macos/scripts/doctor-macos.sh`: validate the installed Codex app, signed bundled Node runtime, theme payload, and optional live session.

Do not bypass failing checks.

## Coding Style & Naming Conventions

Use two-space indentation in shell, JavaScript, JSON, and CSS. Shell entry points use `set -euo pipefail`; Node files use ESM. Follow existing kebab-case script names such as `start-dream-skin-macos.sh`. Prefer existing platform helpers over new dependencies. Keep comments short and focused on safety or non-obvious behavior.

## Testing Guidelines

Tests must cover changed install, start, inject, verify, pause, and restore behavior. For renderer or CSS changes, run live verification and inspect both home and task routes. Configuration tests must include Chinese/non-ASCII project names and prove unrelated TOML content survives install/restore. Never rewrite `config.toml` through an encoding-dependent API; require strict UTF-8, atomic writes, and a recoverable backup.

## Security Constraints

- CDP binds to `127.0.0.1` only; never widen the bind address or accept non-loopback debugger URLs.
- Never modify the official Codex `.app`, `app.asar`, or code signature.
- Never touch API keys, Base URLs, or model provider settings.
- Do not include private chats, API keys, `auth.json`, or personal data in commits.
