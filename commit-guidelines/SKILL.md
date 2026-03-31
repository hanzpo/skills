---
name: commit-guidelines
description: Guidelines for what to include in commit messages. Use when making commits.
---

When writing commit messages, do not add attribution to any co-authors, such as claude. Include only commit messages that follow the conventional commits specification. The specification is as follows: 

# Conventional Commit Messages

## Format

```
<type>(<optional scope>): <description>

<optional body>

<optional footer>
```

## Types

- `feat` — add, adjust, or remove a feature (API/UI relevant)
- `fix` — fix a bug from a previous `feat` commit (API/UI relevant)
- `refactor` — rewrite/restructure code without changing API/UI behavior
- `perf` — a `refactor` that specifically improves performance
- `style` — code style only (whitespace, formatting, semicolons); no behavior change
- `test` — add missing tests or correct existing ones
- `docs` — documentation-only changes
- `build` — build tools, dependencies, project version, etc.
- `ops` — infrastructure, deployment, CI/CD, backups, monitoring, recovery
- `chore` — miscellaneous tasks (init, `.gitignore`, etc.)

## Scopes

- Optional parenthesized context after the type: `feat(auth): ...`
- Scopes are project-specific; do **not** use issue identifiers as scopes.

## Description

- **Mandatory.**
- Imperative, present tense: "change" not "changed" or "changes" (think: *this commit will …*).
- Do not capitalize the first letter.
- Do not end with a period.

## Body

- Optional.
- Explain the motivation for the change and contrast with previous behavior.
- Imperative, present tense.

## Footer

- Optional (unless the commit introduces breaking changes).
- Reference issues: `Closes #123`, `Fixes JIRA-456`.
- Breaking changes must start with `BREAKING CHANGE:` followed by a description.

## Breaking Changes

- Indicated by `!` before the colon: `feat(api)!: remove status endpoint`
- Must be described in the footer if the description alone isn't sufficient.

## Versioning (SemVer)

- Breaking changes → bump **major**.
- API-relevant changes (`feat`, `fix`) → bump **minor**.
- Everything else → bump **patch**.

## Special Commits

Initial commit:

```
chore: init
```

Merge commit (default git message):

```
Merge branch '<branch name>'
```

Revert commit (default git message):

```
Revert "<reverted commit subject line>"
```

## Examples

```
feat: add email notifications on new direct messages
```

```
feat(shopping cart): add the amazing button
```

```
feat!: remove ticket list endpoint

refers to JIRA-1337

BREAKING CHANGE: ticket endpoints no longer supports list all entities.
```

```
fix(shopping-cart): prevent order an empty shopping cart
```

```
fix(api): fix wrong calculation of request body checksum
```

```
fix: add missing parameter to service call

The error occurred due to <reasons>.
```

```
perf: decrease memory footprint for determine unique visitors by using HyperLogLog
```

```
build: update dependencies
```

```
build(release): bump version to 1.0.0
```

```
refactor: implement fibonacci number calculation as recursion
```

```
style: remove empty line
```

## References

- https://www.conventionalcommits.org/
- https://github.com/angular/angular/blob/master/CONTRIBUTING.md
- http://karma-runner.github.io/1.0/dev/git-commit-msg.html
