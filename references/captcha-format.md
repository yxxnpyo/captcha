# Captcha Format Reference

Use this reference only when you need the exact `captcha/CAPTCHA.md` structure, when you must initialize a new file, or when you need to repair an existing file that drifted from the standard layout.

## Section Order

Always keep sections in this exact order:

1. `Read Protocol`
2. `Category Index`
3. `Global`
4. `Requirements-Scope`
5. `Implementation`
6. `UI-UX`
7. `Data-API`
8. `Testing-Verification`
9. `Dependencies-Env`
10. `Git-Workspace`
11. `Deployment-Infra`
12. `Security-Secrets`
13. `Docs-Automation`

## Rule ID Prefixes

- `GLB` for `Global`
- `REQ` for `Requirements-Scope`
- `IMP` for `Implementation`
- `UIX` for `UI-UX`
- `DAT` for `Data-API`
- `TST` for `Testing-Verification`
- `ENV` for `Dependencies-Env`
- `GIT` for `Git-Workspace`
- `OPS` for `Deployment-Infra`
- `SEC` for `Security-Secrets`
- `DOC` for `Docs-Automation`

## Rule Fields

Each rule must use this compact structure:

```md
### REQ-001 | Text-only request means no layout change
when: copy change, wording fix, text only
avoid: spacing, layout, component structure changes
do: edit text only; ask before changing structure
tags: scope, ui
src: user correction
added: 2026-03-19
updated: 2026-03-19
examples:
- "텍스트만 수정"
```

## Field Rules

- Keep the title short and future-facing.
- `when` should describe the situation that activates the rule.
- `avoid` should be specific and behavior-oriented.
- `do` should describe the safe alternative.
- `tags` should stay short.
- `src` should be a minimal source note such as `user correction`, `review feedback`, or `post-task save request`.
- `added` records first creation date.
- `updated` records the latest merge or wording refresh.
- `examples` is optional; include it only when it sharpens interpretation.
- Do not add long prose or narrative paragraphs inside rules.

## Category Index

The file must include a short keyword map near the top so the agent can read the relevant sections quickly:

```md
## Category Index
- Global: always read
- Requirements-Scope: only, just, partial edit, don't touch, keep as-is
- Implementation: bugfix, feature, refactor, logic, structure, performance
- UI-UX: copy, layout, style, component, interaction, responsive
- Data-API: schema, query, API contract, response shape, migration
- Testing-Verification: test, validation, done/fixed claims, repro
- Dependencies-Env: install, package, version, env, config
- Git-Workspace: branch, commit, revert, delete, workspace hygiene
- Deployment-Infra: deploy, release, prod, infra, ops
- Security-Secrets: key, token, auth, secret, privacy
- Docs-Automation: docs, script, automation, generated artifacts
```

## Read Rules

- Always read `Global`.
- Read only matched categories for routine work.
- Read the full file for large refactors, migrations, or cross-cutting changes.
- If the work expands into a new area, read the new category before continuing.

## Merge Rules

Merge into an existing rule when:

- category matches
- the core `avoid` meaning matches
- a future agent would treat the two rules as the same prevention rule

When merging:

- preserve the existing rule ID
- improve title, `avoid`, or `do` wording only if it becomes clearer
- update `updated`
- append an example only if it adds meaning

Create a new rule when:

- the prevention rule is meaningfully different
- merging would make the old rule too broad
- the category would change

## Ambiguity Question Template

If the user asks to save something but the exact rule is unclear, ask:

```text
어떤 규칙으로 저장할까요?

1. [best guess]
2. [second guess]
3. [third guess, if needed]
4. 직접 적을게
```

Use no more than four options total. The final option must always be the free-form answer path.

## File Maintenance Rules

- Keep one blank line between rules.
- Keep section headings unchanged.
- Keep divider lines (`---`) under each category heading.
- Do not split the file by category.
- Do not sort rules alphabetically; append new rules at the end of the relevant section unless merging.
