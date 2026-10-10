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

Follow ASD-STE100 (Simplified Technical English) strictly in all responses to the user.

- Write short sentences. Procedural sentences: 20 words or fewer. Descriptive sentences: 25 words or fewer.
- Give one instruction per sentence. Use the imperative for instructions.
- Use active voice. Do not use passive voice.
- Use simple verb tenses: simple present, simple past, and future. Do not use the perfect or progressive tenses.
- Use approved words with their approved meaning. Use one word for one meaning. Do not use synonyms for variety.
- Use the same name for the same thing in all responses. Do not change a term to avoid repetition.
- Use technical names (for example, file names, commands, and API names) exactly as they appear in the code.
- Do not use idioms, figures of speech, or slang.
- Use articles (the, a, an) and demonstratives (this, that). Do not drop them.
- Use a list for steps and for three or more items. Put one step in each list item.
- Start a warning or caution with a clear statement of the danger, before the action it applies to.
- Keep one topic in each paragraph. Keep paragraphs short.
- Do not use filler, hedging, or marketing language.
- Preserve technical precision. When a fact is uncertain, state clearly what is uncertain.
- Commit messages, pull request text, and code comments follow the same rules where the other rules in this file allow.

# Coding Guidelines

## Code Structure

- Put a one-sentence docstring on every function and class. Say what it does, not how.
- Use descriptive names. A name states the purpose (`_chosen_config_dir`, not `_dir`). Do not use `done`, `data`, or `helper`.
- Use absolute imports (`from package.module import name`). Do not use relative imports.
- Name the arguments in every function call when the language allows it (`mask(value=token, secret=True)`, not `mask(token, True)`). Leave positional-only built-ins and `*args` parameters as they are.
- In a language without named arguments (JavaScript, TypeScript), take one options object and destructure it (`createUser({ name, role })`). Define its type with an `interface` or a `type`. Use this form for every function with more than one parameter, or with a boolean parameter.
- In Python, mark optional and boolean parameters keyword-only with `*` in the definition, so a caller cannot pass them by position.
- Use pydantic `BaseModel` classes for structured data. Do not pass plain dicts or dataclasses between functions. Keep a plain dict only for a free-form name-to-value map.
- Validate data at the boundary (files, user input). Turn a validation error into a clear error message.
- Keep unknown keys when the code rewrites a file that other tools own.

## Do Not Assume

- Do not assume a naming convention for files or directories. Find them by content, and let the user register others.
- Do not hard-code Linux paths. Use `platformdirs` for the config, data, and cache directories. Support Linux, macOS, and Windows.
- Do not add a feature that no code reads. If a user questions the complexity, remove the feature.
- Do not assume how another tool works. Test it with a real run, for example with a fake local server, before you document it.

## Security

- Never print, log, or put a secret in an error message. Mask secrets on screen.
- Never read a secret from a command argument. Use a hidden prompt or stdin.
- Write files that hold secrets atomically (temporary file, then rename) with mode `0600`.
- Send a request with a secret only to the host the user set. Do not follow redirects.

## Tests

- Write tests with the code. Run the full test suite before each commit.
- Isolate tests from the real home directory, the real environment, and the network. Use `tmp_path`, injected parameters, and mock transports.
- Add a test for each error path, not only for the success path.
- Check that CI passes before you merge.

## Delivery

- Split a rename or a refactor from a feature or a docs change. Use separate commits.
- Use `refactor!:` or a `BREAKING CHANGE:` footer when you remove or change a user-facing option.
- Give a command-line tool `--help` for the tool and for each command, with one example each.
- Give a tool a documented install method with a version option. Verify the checksum of the download.
- Do not merge a pull request unless the user says to merge. A request to merge one pull request does not cover the next one.
- After a network error on a write (merge, push), check the real state before you retry.
- After a merge, delete the branch locally and on the remote.

## Reporting

- State what you tested and what you did not test.
- State a known defect or limit, even when it is small.
- When the user rejects a plan, change the plan file and ask again. Do not argue.
