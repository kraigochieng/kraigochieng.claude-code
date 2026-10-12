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

## Agnosticism

- Write each guideline so that it applies to any language, framework, and tool.
- State a rule as a principle. Do not name a language, framework, library, or tool in the rule.
- Put a language-specific detail in an example. Mark the example with "for example".
- Put a rule that applies to one language in a section that names the language.
- Before you add a rule, ask: "Does this rule hold in another language?" If not, make it an example or a language section.

## Code Structure

- Put a one-sentence doc comment on every function and class. Say what it does, not how.
- Use descriptive names. A name states the purpose (for example, `_chosen_config_dir`, not `_dir`). Do not use `done`, `data`, or `helper`.
- Use absolute imports. Do not use relative imports.
- Name the arguments in every function call when the language allows it (for example, `mask(value=token, secret=True)`, not `mask(token, True)`). Leave positional-only built-ins and variadic parameters as they are.
- In a language without named arguments, take one options object and destructure it. Define its type. Use this form for every function with more than one parameter, or with a boolean parameter.
- When the language allows it, mark optional and boolean parameters so that a caller cannot pass them by position.
- Give every function explicit types: each parameter and the return value. Do not leave a type to inference at a function boundary. Do not use a catch-all type or an untyped collection. Write the element types.
- Give every variable an explicit type, not only every function. This covers constants, class variables, type aliases, and local variables. Declare a name once, at its first assignment in the scope. Do not repeat the type when you rebind it. Do not rebind a parameter with a new type. Use a new name.
- Some names cannot take an inline type: loop targets, `with ... as` names, `except ... as` names, and tuple-unpack targets. Leave them to inference.
- Check the types with a strict type checker in CI. Run a linter in CI that requires types on functions. Note: no linter requires a type on every local variable, so check this rule in review. Do not pin the language version in the checker config. Test on every language version that CI runs.
- In a typed language, types are always required. Turn on the strict mode of the compiler or checker. Do not use the catch-all type.
- Use declared model types for structured data. Do not pass plain maps or unvalidated records between functions. Keep a plain map only for a free-form name-to-value map.
- Validate data at the boundary (files, user input). Turn a validation error into a clear error message.
- Keep unknown keys when the code rewrites a file that other tools own.

## Structure

- Give each module, class, and function one responsibility. A responsibility is one reason to change.
- State the responsibility in one sentence without the word "and". If the sentence needs "and", split the unit.
- Treat size as a symptom, not as a goal. A module of more than about 300 lines, or a function of more than about 60 lines, probably has a second responsibility. Look for it. Do not cut at a line count.
- Before you write code, list the units and the one-sentence responsibility of each.
- Put new code in the unit that owns the responsibility. If no unit owns it, create a new unit. Do not append the code to the nearest large file.
- Name a unit by its responsibility (for example, `parser`, `variables`). Do not use `utils`, `helpers`, or `misc`.
- Let dependencies point one way. A shared helper does not import from the code that uses it.
- Merge code that three places repeat. Leave code that two places repeat until a third place needs it.

## Data Access

- Put all data access in a repository. The repository owns the queries and the storage calls.
- Do not read or write the data store outside a repository.
- Give the repository a typed interface. Return the structured types of the project, not raw rows.

## Refactoring

- A refactor changes the structure and never the behavior.
- Separate a move from a change. One commit moves code. Another commit changes it.
- Keep the public interface: import paths, entry points, command options, and output. Mark a commit `refactor!:` when it changes the interface.
- Prove that the behavior is the same. The same tests pass. Edit a test only for an import path or a patch target, and name each edit in the pull request. Compare the output before and after (help text, screenshots, written files).
- Check that a comparison loads both versions. A comparison that loads the same code twice proves nothing.
- Work in small steps. Each commit builds and passes the tests. Use one pull request for each module or package.
- Do not mix a refactor and a feature. If the structure blocks a feature, refactor first.

## Do Not Assume

- Do not assume a naming convention for files or directories. Find them by content, and let the user register others.
- Do not hard-code the paths of one operating system. Use the platform library for the config, data, and cache directories. Support Linux, macOS, and Windows.
- Do not add a feature that no code reads. If a user questions the complexity, remove the feature.
- Do not assume how another tool works. Test it with a real run, for example with a fake local server, before you document it.

## Security

- Never print, log, or put a secret in an error message. Mask secrets on screen.
- Never read a secret from a command argument. Use a hidden prompt or stdin.
- Write files that hold secrets atomically (temporary file, then rename) with owner-only permissions (for example, mode `0600`).
- Send a request with a secret only to the host the user set. Do not follow redirects.

## User Interface

- Ask for confirmation before every destructive action. Name the item in the confirmation.
- Give every table pagination, sorting, filtering, and search. Keep the values of these four in the URL query parameters.
- Save the input of a form as the user types. Restore the input when the user returns to the page. Clear the saved input when the form submits.
- Do not save a secret field in the saved form input.
- Give every number input with a limited range a slider.
- Give every free-text input a clear option.

## Tests

- Write tests with the code. Run the full test suite before each commit.
- Isolate tests from the real home directory, the real environment, and the network. Use temporary directories, injected parameters, and mock transports.
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

## Python

- Mark optional and boolean parameters keyword-only with `*` in the definition, so a caller cannot pass them by position.
- Use absolute imports (`from package.module import name`).
- Do not use `Any`, `object` as a shortcut, or an untyped `dict` or `list`. Write the element types (`dict[str, int]`).
- Hint constants with `Final[str]`, class variables with `ClassVar[...]`, and type aliases with `TypeAlias`. Hint a local variable at its first assignment (`checks: list[Check] = []`).
- Check the types with `mypy --strict` (or an equal strict checker) in CI. Run `ruff check` with the `F`, `I`, and `ANN` rules in CI.
- Do not pin `python_version` in the checker config. Test on every Python version that CI runs.
- Use pydantic `BaseModel` classes for structured data. Do not pass plain dicts or dataclasses between functions.
- Use `platformdirs` for the config, data, and cache directories.
- Use `tmp_path` to isolate tests from the real home directory.

## TypeScript

- Take one options object and destructure it (`createUser({ name, role })`). Define its type with an `interface` or a `type`.
- Set `strict: true`. Do not use `any`.
