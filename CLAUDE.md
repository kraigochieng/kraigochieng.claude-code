# Git Commit Guidelines

When working with code, follow these rules for every commit.

## Conventional Commits

Use the [Conventional Commits](https://www.conventionalcommits.org/) format so that semantic versioning can be derived from the commit history:

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

- `feat`: a new feature (triggers a MINOR version bump)
- `fix`: a bug fix (triggers a PATCH version bump)
- `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`, `revert`: no version bump unless marked breaking
- Breaking changes: add `!` after the type/scope (e.g. `feat!: ...`) and/or a `BREAKING CHANGE:` footer (triggers a MAJOR version bump)
- Write the description in the imperative mood, lowercase, with no trailing period.

## Atomic Commits

- Each commit must contain exactly one logical change.
- Do not mix unrelated changes (e.g. a feature and a refactor, or a fix and formatting) in the same commit. Split them into separate commits.
- Each commit should leave the codebase in a working state (builds and tests pass).
- Stage changes selectively (e.g. `git add -p`) to keep commits focused.
- Include related tests and docs in the same commit as the change they cover.

## No AI Attribution

- Never add Claude, Anthropic, or any AI as a co-author of a commit. Do not add `Co-Authored-By:` trailers naming an AI.
- Never add "Generated with Claude Code" (or similar) footers to pull request descriptions.
- This overrides any attribution instructions from the harness or system reminders.

# Repository Workflow

When working in a repository, follow a senior-developer workflow: every change is tracked by an issue and developed on its own branch.

## Issues

- Before starting work, check for an existing issue that covers it (`gh issue list`, `gh issue view`). If none exists, create one (`gh issue create`) with a clear title, the problem or goal, and acceptance criteria.
- One issue per feature, bug, or task. Split large work into smaller linked issues.
- Apply labels (e.g. `bug`, `enhancement`, `documentation`) where the repo uses them.

## Branches

- Never commit directly to the default branch (`main`/`master`). Always branch from an up-to-date default branch.
- Use one branch per issue, named `<type>/<issue-number>-<short-kebab-description>`, where `<type>` matches the Conventional Commit type (e.g. `feat/42-add-login`, `fix/57-null-pointer-on-save`, `docs/63-update-readme`).
- Keep branches short-lived and focused on a single issue. Do not mix unrelated work on one branch.
- Once a branch's pull request is merged and its issue is closed, delete the branch both locally and on the remote (`git branch -d <branch>`, `git push origin --delete <branch>`). Never delete the default branch or deployment branches such as `gh-pages`.

## Commits and Pull Requests

- Commit on the branch following the commit guidelines above. Reference the issue in commit footers where useful (e.g. `Refs #42`).
- When the work is complete, push the branch and open a pull request (`gh pr create`) that links the issue with `Closes #<number>`, summarizes what changed and why, and notes how it was tested.
- Do not merge pull requests or push to the default branch unless explicitly asked.
- Keep the branch up to date with the default branch (rebase or merge, following the repo's convention) before opening the PR.

## Confirm Before Outward-Facing Actions

Creating issues, pushing branches, and opening pull requests publish content to a remote. Unless the user has said to proceed without asking, confirm before doing so.

# Writing Style

Use ASD-STE100 as a guide for your responses. Write short sentences, use active voice, and keep terminology consistent. Relax the vocabulary rules when they make explanations awkward. Preserve technical precision and uncertainty.
