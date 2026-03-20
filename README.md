# memento

[Korean README / 한국어 버전 README](./README_ko.md)

`memento` is a reusable Codex skill for storing repository-specific "do-not-repeat" rules in a single file and reusing them before future work.

## What It Does

When a user says things like `save this to memento`, `remember this rule`, `don't do this again`, `add this to the repo memento`, or asks the agent to remember a mistake, the skill:

1. Looks at the recent work context.
2. Extracts what should not be repeated.
3. Rewrites it as a reusable rule.
4. Stores it in `memento/MEMENTO.md` inside the target repository.

Later, when the agent starts planning, editing, or verifying work in the same repository, it reads that rulebook first and avoids repeating the stored mistakes.

## Why It Exists

This skill gives each repository its own lightweight memory for:

- recurring mistakes
- scope-control rules
- validation rules
- risky actions to avoid
- project-specific exclusions

It helps the agent stay aligned with repository-specific expectations without relying only on short-term conversation context.

## Installation

Install from GitHub with `skills.sh`:

```bash
npx skills add https://github.com/yxxnpyo/memento
```

If you are developing locally or copying files manually, place the skill in your shared skills directory or workspace skill collection:

```text
skills/
  memento/
    SKILL.md
    README.md
    README_ko.md
    references/
      memento-format.md
    assets/
      MEMENTO.template.md
```

Required files:

- `SKILL.md`
- `references/memento-format.md`
- `assets/MEMENTO.template.md`

## How It Works

### 1. Saving a rule

When the user asks to save a mistake or exclusion, the skill creates or updates:

```text
memento/MEMENTO.md
```

Rules are stored in one file only. The skill does not create one file per category.

### 2. Reading before work

If `memento/MEMENTO.md` already exists in a repository, the agent:

- always reads `Global`
- reads only task-relevant categories for normal work
- reads the full file for broad refactors or migrations

### 3. Auto-categorization

The user does not need to choose a category. The agent automatically places rules into sections such as:

- `Requirements-Scope`
- `Implementation`
- `UI-UX`
- `Data-API`
- `Testing-Verification`
- `Deployment-Infra`

### 4. Merge-over-duplicate behavior

If a similar rule already exists, the skill updates the existing rule instead of adding noisy duplicates.

## Typical User Phrases

- `save this to memento`
- `remember this rule`
- `don't do this again`
- `add this to the repo memento`
- `keep this in memento`
- `store this as a repo rule`
- `remember this for future work`

## Ambiguity Handling

If it is not clear what the user wants excluded, the skill asks a short multiple-choice question.

The last option is always a free-form answer so the user can type the exact rule directly.

## Output Format

The repository-local rulebook lives at:

```text
memento/MEMENTO.md
```

It is designed for fast scanning by agents:

- one file only
- fixed category order
- short rule fields
- compact `avoid` / `do` structure

See [`references/memento-format.md`](./references/memento-format.md) for the exact format.

## Effect

Using `memento` improves consistency over time by making repository-specific lessons persistent and reusable.

In practice, it helps reduce:

- repeated scope mistakes
- unnecessary UI or implementation drift
- verification omissions
- risky or unapproved actions
- repeated user corrections on the same repository
