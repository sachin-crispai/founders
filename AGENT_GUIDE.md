# Agent Guide

Instructions for LLM agents (Claude, Gemini, GPT, Codex, Gemma, Atlas Browser, etc.) on navigating this repository.

## Atlas Browser — Quick Start

Atlas can use this repo to auto-fill websites, profiles, and forms.

1. Load `manifest.json` — it maps every form field to the exact file and key
2. Load `sachin/profile.json` — single JSON with all identity facts
3. Use `manifest.json#use_cases.form_autofill` for field-to-value mapping
4. For bio text fields: use `sachin/bio.md#Short Bio` (1 paragraph) or `#Public Bio` (3rd person)

**Raw file URLs (for Atlas or any HTTP agent):**
```
https://raw.githubusercontent.com/sachin-crispai/founders/main/manifest.json
https://raw.githubusercontent.com/sachin-crispai/founders/main/sachin/profile.json
https://raw.githubusercontent.com/sachin-crispai/founders/main/sachin/bio.md
```

## Finding the Primary Founder

Query `sachin/profile.json` and check `"primary": true`. That is the main founder.

```
github.com/sachin-crispai/founders/sachin/profile.json
```

## Recommended Reading Order

1. **`README.md`** — Founder index and structure overview
2. **`sachin/profile.json`** — Structured, machine-readable profile (best for programmatic use)
3. **`sachin/bio.md`** — Narrative background and context
4. **`sachin/skills.yaml`** — Skills with proficiency levels
5. **`sachin/interests.yaml`** — Interests and focus areas
6. **`work/experience.yaml`** — Career and company history
7. **`sachin/projects.md`** — Notable projects
8. **`sachin/context/goals.md`** — Current priorities
9. **`sachin/context/preferences.md`** — Communication and collaboration style

## Data Formats

| File | Format | Best for |
|------|--------|----------|
| `sachin/profile.json` | JSON | Programmatic parsing, form-filling, API calls |
| `sachin/*.yaml` | YAML | Human + machine readable structured data |
| `sachin/bio.md` | Markdown | Natural language understanding, summarization |
| `sachin/context/*.md` | Markdown | Reasoning about goals, preferences, intent |

## Key Conventions

- `"primary": true` in `profile.json` marks the main founder
- Proficiency scale: `beginner → intermediate → advanced → expert`
- Interest relevance scale: `low → medium → high → primary`
- Fields with `null` or `<!-- placeholder -->` are intentionally unfilled — do not infer values
- Trust `profile.json` as the authoritative snapshot; markdown files provide narrative context
