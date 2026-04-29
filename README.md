# Atomic Framework - GitHub Copilot Skills

Agent skills for **[Atomic Framework](https://github.com/MADEVAL/Atomic-Framework)** - a modular PHP 8.1+ framework built on [Fat-Free Framework](https://fatfreeframework.com/) modern verion [Fat-Free Framework Modern](https://github.com/MADEVAL/fat-free-framework).

Each skill is a `SKILL.md` file that GitHub Copilot agent loads to get accurate, verified knowledge about one area of the framework. Skills replace guesswork with ground-truth API references pulled directly from the engine source.

---

## Installation

Copy the skills folder into your project or configure VS Code to load skills from a shared path:

```jsonc
// .vscode/settings.json
{
    "github.copilot.chat.skills.instructionFilesGlob": "skills/**/*.md"
}
```

Or clone this repository directly and point Copilot at it.

---

## Skills Index

| Skill folder | What it covers |
|---|---|
| [`atomic-framework-overview`](./atomic-framework-overview/SKILL.md) | Architecture, module map, bootstrap chain, routing conventions, hive basics. **Start here.** |
| [`atomic-framework-core`](./atomic-framework-core/SKILL.md) | Config loading, middleware, logging, guard, crypto, DB connections, migrations, request/response, upload, ID, filesystem, redactor |
| [`atomic-framework-app-auth`](./atomic-framework-app-auth/SKILL.md) | Controllers, app models, auth system, Google/Telegram OAuth, user roles, session, error pages |
| [`atomic-framework-data`](./atomic-framework-data/SKILL.md) | Models (Cortex ORM), validation, enums, exceptions, PDF/XLS/CSV export |
| [`atomic-framework-cli-api`](./atomic-framework-cli-api/SKILL.md) | CLI commands (`php atomic ...`), API entrypoint, console output helpers, scaffolding |
| [`atomic-framework-event-hook-lang-mail`](./atomic-framework-event-hook-lang-mail/SKILL.md) | Event bus, WordPress-style hooks/filters, i18n, SMTP mailer, notifier |
| [`atomic-framework-mutex-session`](./atomic-framework-mutex-session/SKILL.md) | Distributed mutex, session drivers (SQL/Redis), nonce, transient cache |
| [`atomic-framework-queue-scheduler-telemetry`](./atomic-framework-queue-scheduler-telemetry/SKILL.md) | Job queue, workers, scheduler (cron-style), telemetry diagnostics panel |
| [`atomic-framework-theme`](./atomic-framework-theme/SKILL.md) | Theme boot, Head (meta/SEO tags), asset enqueue, OpenGraph, JSON-LD schema |
| [`atomic-framework-plugins`](./atomic-framework-plugins/SKILL.md) | Plugin lifecycle, PluginManager, built-in integrations: Monopay, WordPress, WooCommerce, RSS Reader, GlobusStudio |
| [`atomic-framework-tools-websockets`](./atomic-framework-tools-websockets/SKILL.md) | AI Connector (OpenAI/Groq/OpenRouter/Globus), WebSocket server, Telegram bot, nonce, transient |
| [`atomic-framework-doc-map`](./atomic-framework-doc-map/SKILL.md) | Cross-reference table: doc file → engine path → skill. Use to navigate docs. |

---

## How Skills Work

A skill is a plain Markdown file with YAML frontmatter:

```yaml
---
name: atomic-framework-core
description: "Use when working with..."
argument-hint: "Bootstrap, config, logging, routing"
user-invocable: true
---
```

GitHub Copilot agent reads the skill on demand and uses its code examples and API references to generate accurate completions. Skills are **not auto-loaded** - Copilot picks the right one based on the `description` field or you can invoke a skill explicitly by name.

---

## Skill Selection Guide

> Not sure which skill to load? Start with `atomic-framework-overview`.

| You are working on... | Load skill |
|---|---|
| Bootstrap, app init, routing, middleware | `atomic-framework-core` |
| Controllers, user auth, roles, OAuth | `atomic-framework-app-auth` |
| Database models, validation, enums | `atomic-framework-data` |
| CLI commands, `php atomic ...` | `atomic-framework-cli-api` |
| Events, hooks, filters | `atomic-framework-event-hook-lang-mail` |
| i18n, translation, locales | `atomic-framework-event-hook-lang-mail` |
| Sending email | `atomic-framework-event-hook-lang-mail` |
| Mutex, session, nonce | `atomic-framework-mutex-session` |
| Background jobs, cron | `atomic-framework-queue-scheduler-telemetry` |
| Themes, layouts, SEO meta | `atomic-framework-theme` |
| Plugins, 3rd-party integrations | `atomic-framework-plugins` |
| AI chat, WebSockets, Telegram | `atomic-framework-tools-websockets` |
| Finding a doc file | `atomic-framework-doc-map` |

---

## Framework

Source: [https://github.com/MADEVAL/Atomic-Framework](https://github.com/MADEVAL/Atomic-Framework)

Engine entry: `engine/Atomic/` - 25 component folders.
Global helpers: `engine/Atomic/Support/helpers.php`.
Docs: `docs/` - 44 Markdown files covering all subsystems.

---

## Contributing

Skills are manually audited against the engine source. If you find an inaccuracy:

1. Check `engine/Atomic/<Component>/<File>.php` for the ground truth.
2. Update the relevant `SKILL.md` section.
3. Add a `## Guardrails` note if the mistake is easy to repeat.

Do not add methods or helpers that do not exist in the source.
