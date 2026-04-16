# Agent Guide

Instructions for LLM agents (Claude, Gemini, GPT, Codex, Gemma, etc.) on navigating this repository.

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
