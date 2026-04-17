# Agent Workflow

Step-by-step instructions for any LLM agent (Claude, GPT, Gemini, Gemma, Codex, Atlas) taking over work in this repository.

---

## Task 1: Orient Yourself (always do this first)

```
DAG: read manifest → read profile → read preferences → proceed
```

1. Read `manifest.json` — understand what files exist and why
2. Read `sachin/profile.json` — get identity facts (name, email, role, links)
3. Read `sachin/context/preferences.md` — understand how Sachin wants agents to work
4. Read `sachin/context/goals.md` — understand current priorities before making suggestions

**Rule:** Never make recommendations without reading goals first. CrispAI is targeting a niche acquisition — suggestions should align with that.

---

## Task 2: Form Autofill (Atlas Browser / web agents)

```
DAG: load profile.json → map fields → fill form → confirm
```

Use `manifest.json#use_cases.form_autofill` to map form fields to profile values.

| Form Field | Source |
|-----------|--------|
| First Name | `profile.json → identity.first_name` = `Sachin` |
| Last Name | `profile.json → identity.last_name` = `Naik` |
| Full Name | `profile.json → identity.name` = `Sachin Naik` |
| Email | `profile.json → identity.email` = `sachin@crispai.com` |
| Company | `profile.json → identity.company` = `CrispAI` |
| Title / Role | `profile.json → identity.role` = `Co-Founder / CTO` |
| Headline | `profile.json → identity.headline` |
| Location | `profile.json → identity.location` = `San Francisco Bay Area, California, USA` |
| LinkedIn | `profile.json → links.linkedin` |
| GitHub | `profile.json → links.github` |
| Twitter | `profile.json → links.twitter` = `@sachinnaik` |
| Short Bio | `bio.md → ## Short Bio` |
| Public Bio | `bio.md → ## Public Bio` |

**Rule:** If a field is `null` in `profile.json`, do not guess — leave it blank or ask Sachin.

---

## Task 3: Update Profile Information

```
DAG: identify change → edit source file → sync profile.json → commit → push
```

1. **Single source of truth:** `sachin/profile.json` for structured facts, markdown files for narrative
2. **Always update `profile.json`** when identity facts change (name, role, location, links)
3. **Always update `_meta.last_updated`** in any file you edit
4. **Commit message format:**
   ```
   <what changed>: <one-line reason>
   ```
5. **Push after every commit** — this repo is consumed live by Atlas and other agents

**Which file to edit for what:**

| Change | Edit This File |
|--------|---------------|
| New job / role | `work/experience.yaml` + `sachin/profile.json` |
| New skill | `sachin/skills.yaml` + `sachin/profile.json#skills` |
| New project | `sachin/projects.md` + `work/projects.md` |
| Goals changed | `sachin/context/goals.md` + `profile.json#goals` |
| New certificate | `work/experience.yaml#certifications` |
| Bio update | `sachin/bio.md` |
| Link update | `sachin/profile.json#links` + `sachin/README.md` |

---

## Task 4: Add a New Founder Profile

```
DAG: create <name>/ dir → copy sachin/ structure → fill profile.json (primary: false) → update root README.md
```

1. Create `<founder-name>/` directory mirroring `sachin/` structure
2. Set `"primary": false` in their `profile.json`
3. Add a row to the Founders table in root `README.md`
4. Do NOT modify `sachin/` files

---

## Task 5: Answer Questions About Sachin

```
DAG: check profile.json → check relevant yaml/md → synthesize → respond
```

- **Technical skills?** → `sachin/skills.yaml`
- **Career history?** → `work/experience.yaml`
- **Current goals?** → `sachin/context/goals.md`
- **How to work with him?** → `sachin/context/preferences.md`
- **Projects?** → `sachin/projects.md`
- **Quick facts?** → `sachin/profile.json`

---

## Error Recovery

If you encounter missing or `null` data:
1. Check if another file has the value (e.g., `bio.md` may have narrative form of a null JSON field)
2. Do not hallucinate values — use `null` or leave blank
3. Flag the gap: add a `# TODO:` comment in the file and note it in your response

If a git push fails:
1. Run `git pull --rebase` first
2. Resolve conflicts by preferring the more recently dated content
3. Re-push

---

## Conventions

- **Proficiency scale:** `beginner → intermediate → advanced → expert`
- **Relevance scale:** `low → medium → high → primary`
- **Primary founder flag:** `"primary": true` in `profile.json`
- **Dates:** ISO format `YYYY-MM` for month precision, `YYYY` for year only
- **Null fields:** `null` in JSON, blank after `:` in YAML — never guess
- **Comments in YAML:** Use `#` for agent-facing notes, not inline data

---

## Handoff Checklist

Before handing off to another agent, verify:

- [ ] `sachin/profile.json` reflects latest facts
- [ ] `_meta.last_updated` is current in edited files
- [ ] All changes committed and pushed to `github.com/sachin-crispai/founders`
- [ ] No `null` fields introduced without a `# TODO:` comment
- [ ] `manifest.json` updated if new files were added
