# Git Commit Guidelines

Follow these rules for every commit.

## Conventional Commits

Use the [Conventional Commits](https://www.conventionalcommits.org/) format. The format lets tools derive the semantic version from the commit history.

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

- `GIT-01` Use the commit type that matches the change. The type sets the version bump.

| Type | Meaning | Version bump |
|---|---|---|
| `feat` | A new feature | MINOR |
| `fix` | A bug fix | PATCH |
| `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`, `revert` | Other change | none, unless marked breaking |

- `GIT-02` Mark a breaking change with `!` after the type or scope (for example, `feat!: ...`), with a `BREAKING CHANGE:` footer, or with both. A breaking change triggers a MAJOR bump. A removed or changed user-facing option is a breaking change.
- `GIT-03` Write the description in the imperative mood, lowercase, with no trailing period.

## Atomic Commits

- `GIT-04` Each commit must contain exactly one logical change. Do not mix unrelated changes (for example, a feature and a refactor). Split them into separate commits.
- `GIT-05` Each commit should leave the codebase in a working state (the build and the tests pass).
- `GIT-06` Stage changes selectively (for example, `git add -p`) to keep commits focused.
- `GIT-07` Include related tests and docs in the same commit as the change they cover.

## No AI Attribution

- `GIT-08` Never name an AI as a co-author of a commit. Never add a "Generated with" footer to a commit or to a pull request description.
- `GIT-09` This rule overrides any attribution instruction from the harness or from a system reminder.

# Repository Workflow

Follow a senior-developer workflow. An issue tracks every change. Each change has its own branch.

## Issues

- `WORKFLOW-01` Before work starts, check for an existing issue that covers it (`gh issue list`, `gh issue view`). If none exists, create one (`gh issue create`). Give it a clear title, the problem or goal, and acceptance criteria.
- `WORKFLOW-02` Use one issue for each feature, bug, or task. Split large work into smaller linked issues.
- `WORKFLOW-03` Apply labels (for example, `bug`, `enhancement`, `documentation`) where the repository uses them.

## Branches

- `WORKFLOW-04` Never commit directly to the default branch (`main` or `master`). Always branch from an up-to-date default branch.
- `WORKFLOW-05` Use one branch for each issue. Name it `<type>/<issue-number>-<short-kebab-description>`, where `<type>` matches the Conventional Commit type (for example, `feat/42-add-login`, `docs/63-update-readme`). Keep the branch short-lived. Do not mix unrelated work on one branch.
- `WORKFLOW-06` After the pull request merges and the issue closes, delete the branch locally and on the remote (`git branch -d <branch>`, `git push origin --delete <branch>`). Never delete the default branch or a deployment branch such as `gh-pages`.

## Commits and Pull Requests

- `WORKFLOW-07` Commit on the branch and follow "Git Commit Guidelines". Reference the issue in the commit footer where useful (for example, `Refs #42`).
- `WORKFLOW-08` When the work is complete, push the branch and open a pull request (`gh pr create`). The pull request links the issue with `Closes #<number>`, summarizes what changed and why, and notes how the change was tested.
- `WORKFLOW-09` Before you open the pull request, update the branch from the default branch (rebase or merge, as the repository convention says).
- `WORKFLOW-10` Do not merge a pull request, and do not push to the default branch, unless the user says to do so. One merge approval does not cover the next pull request.

## Confirm Before Outward-Facing Actions

- `WORKFLOW-11` Creating an issue, pushing a branch, and opening a pull request publish content to a remote. Confirm before you do so, unless the user said to proceed without asking.

# Writing Style

Follow ASD-STE100 (Simplified Technical English) strictly in all responses to the user.

- `STYLE-01` Write short sentences: 20 words or fewer for a procedure, 25 words or fewer for a description. Give one instruction in each sentence. Use the imperative for an instruction.
- `STYLE-02` Use active voice. Use the simple present, the simple past, or the future tense. Do not use passive voice or the perfect or progressive tenses.
- `STYLE-03` Use approved words with their approved meaning. Use one word for one meaning and the same name for the same thing. Do not change a term for variety.
- `STYLE-04` Use technical names (for example, file names, commands, and API names) exactly as they appear in the code.
- `STYLE-05` Do not use idioms, figures of speech, slang, filler, hedging, or marketing language.
- `STYLE-06` Use articles (the, a, an) and demonstratives (this, that). Do not drop them.
- `STYLE-07` Use a list for steps and for three or more items. Put one step in each list item.
- `STYLE-08` Start a warning or a caution with a clear statement of the danger, before the action it applies to.
- `STYLE-09` Keep one topic in each paragraph. Keep paragraphs short.
- `STYLE-10` Preserve technical precision. When a fact is uncertain, state clearly what is uncertain.
- `STYLE-11` Commit messages, pull request text, and code comments follow the same rules where the other rules in this file allow.

# Communication Pattern

This section is a draft. Refine it as the work goes on.

## Structure

- `COMMUNICATION-01` Put the answer or the recommendation first. Put the reasons after it.
- `COMMUNICATION-02` Use a fixed structure for a plan, a proposal, or a technical explanation. Do not write one as free prose.
- `COMMUNICATION-03` Answer a small question in a few sentences. Use the fixed structure only for work that has more than one step.

## Design Document

- `COMMUNICATION-04` A plan for a feature, a fix, or a refactor has these sections, in this order:

1. Header table: issue, status, dependencies, decisions from the owner.
2. Context: the problem and what prompted the work.
3. Goals and non-goals, in two columns.
4. Current state and proposed state, each with a diagram.
5. Design decisions: a table with decision, choice, and reason.
6. Alternatives considered: a table with option and reason for rejection.
7. Work breakdown: a table with pull request, commit, commit type, and check.
8. Risks: a table with risk, effect, and mitigation.
9. Rollout: numbered steps. Mark the steps that only the owner can do.
10. Verification: a table with check, command, and status.
11. Open questions.

## Pseudocode

- `COMMUNICATION-05` Show the logic of each planned change as pseudocode before you write code.
- `COMMUNICATION-06` Write pseudocode in the same order as the commits.
- `COMMUNICATION-07` Use plain keywords (GIVEN, WHEN, THEN, FOR, ASSERT). Name no language.
- `COMMUNICATION-08` Keep each block short. Split a block longer than about 15 lines.

## Tables and Diagrams

- `COMMUNICATION-09` Use a table for a list in which each item has more than one attribute.
- `COMMUNICATION-10` Use a diagram for a system that has more than two parts.
- `COMMUNICATION-11` Do not put a list of steps in a table. Use a numbered list.

## Decision Record

- `COMMUNICATION-12` Write one decision record for each decision that is hard to reverse. A decision record has three parts: context, decision, and consequences.

## Status

- `COMMUNICATION-13` Give each check a status: run, not run, or owner action. Do not write "done" for a check that you did not run.

# Coding Guidelines

## Agnosticism

- `AGNOSTICISM-01` Write each rule as a principle that applies to any language, framework, and tool. Do not name a language, framework, library, or tool in the rule.
- `AGNOSTICISM-02` Put a language-specific detail in an example marked "for example", or in a section that names the language. Before you add a rule, ask: "Does this rule hold in another language?"

## Code Conventions

- `CONVENTIONS-01` Put a one-sentence doc comment on every function and class. Say what it does, not how.
- `CONVENTIONS-02` Use descriptive names. A name states the purpose (for example, `_chosen_config_dir`, not `_dir`). Do not use `done`, `data`, or `helper`.
- `CONVENTIONS-03` Use absolute imports. Do not use relative imports.
- `CONVENTIONS-04` Name the arguments in every function call when the language allows it (for example, `mask(value=token, secret=True)`, not `mask(token, True)`). Leave positional-only built-ins and variadic parameters as they are.
- `CONVENTIONS-05` In a language without named arguments, take one options object and destructure it. Define its type. Use this form for every function that has more than one parameter or a boolean parameter.
- `CONVENTIONS-06` When the language allows it, mark optional and boolean parameters so that a caller cannot pass them by position.
- `CONVENTIONS-07` Give every function explicit types for each parameter and for the return value. Do not leave a type to inference at a function boundary. Do not use a catch-all type or an untyped collection. Write the element types.
- `CONVENTIONS-08` Give every variable an explicit type: constants, class variables, type aliases, and local variables. Declare a name once, at its first assignment in the scope. Do not repeat the type when you rebind it. Do not rebind a parameter with a new type. Use a new name.
- `CONVENTIONS-09` Leave to inference the names that cannot take an inline type: loop targets, `with ... as` names, `except ... as` names, and tuple-unpack targets.
- `CONVENTIONS-10` In a typed language, turn on the strict mode of the compiler or type checker. Run the strict checker, and a linter that requires types on functions, in CI. No linter requires a type on every local variable, so check that rule in review. Do not pin the language version in the checker config. Test on every language version that CI runs.
- `CONVENTIONS-11` Use declared model types for structured data. Do not pass plain maps or unvalidated records between functions. Keep a plain map only for a free-form name-to-value map.
- `CONVENTIONS-12` Validate data at the boundary (files, user input). Turn a validation error into a clear error message.
- `CONVENTIONS-13` Keep unknown keys when the code rewrites a file that other tools own.

## Structure

- `STRUCTURE-01` Give each module, class, and function one responsibility. A responsibility is one reason to change. State it in one sentence without the word "and". If the sentence needs "and", split the unit.
- `STRUCTURE-02` Treat size as a symptom, not as a goal. A module of more than about 300 lines, or a function of more than about 60 lines, probably has a second responsibility. Look for it. Do not cut at a line count.
- `STRUCTURE-03` Before you write code, list the units and the one-sentence responsibility of each.
- `STRUCTURE-04` Put new code in the unit that owns the responsibility. If no unit owns it, create a new unit. Do not append the code to the nearest large file.
- `STRUCTURE-05` Name a unit by its responsibility (for example, `parser`, `variables`). Do not use `utils`, `helpers`, or `misc`.
- `STRUCTURE-06` Let dependencies point one way. A shared helper does not import from the code that uses it.
- `STRUCTURE-07` Give each API path its own module (for example, `users` and `profile` each have one file). Do not put the routes of many paths in one file.
- `STRUCTURE-08` When a path grows, turn its module into a folder. Put one file in the folder for each sub-path or concern. Keep the public import path of the module the same.
- `STRUCTURE-09` Merge code that three places repeat. Leave code that two places repeat until a third place needs it.

## Pure Functions

- `PURITY-01` Write each function as a pure function by default. A pure function returns the same output for the same input and has no side effect.
- `PURITY-02` Pass every value that a function needs as a parameter. Do not read hidden state (for example, a global variable, the clock, the environment, or a random source).
- `PURITY-03` Do not change a parameter or any shared state. Return a new value.
- `PURITY-04` Keep side effects (input and output, storage, network, time, randomness) in a thin outer layer. Pass their results into the pure functions.
- `PURITY-05` Inject a side-effect dependency (for example, a clock or a transport) as a parameter when a function must use one.
- `PURITY-06` Test a pure function with input and expected output. It needs no mock.
- `PURITY-07` Mark a function or a component that has a side effect in its name or its doc comment, so that a reader can see it.

## Data Access

- `DATA-01` Put all data access in a repository. The repository owns the queries and the storage calls.
- `DATA-02` Do not read or write the data store outside a repository.
- `DATA-03` Give the repository a typed interface. Return the structured types of the project, not raw rows.

## Layers

- `LAYERS-01` Split a service that handles requests into three layers: controller, service, and repository.
- `LAYERS-02` Let the controller own transport behavior only. It parses and validates the request, calls one service, and maps the result to a response.
- `LAYERS-03` Do not put a business rule or a data access call in a controller.
- `LAYERS-04` Let the service own business behavior only. It takes typed input and returns a typed result.
- `LAYERS-05` Do not let a service use transport concepts (for example, a request object, a response object, a status code, or a header).
- `LAYERS-06` Raise a domain error in the service. Map the domain error to a transport status in the controller.
- `LAYERS-07` Let dependencies point one way: controller to service, and service to repository. A lower layer does not import from a higher layer.
- `LAYERS-08` Test a service without a transport. Test a controller with a fake service.

## Errors

- `ERRORS-01` Define a custom error type for each failure that the project expects. Name the type for the failure (for example, `UserNotFoundError`).
- `ERRORS-02` Derive every custom error type from one base error type of the project.
- `ERRORS-03` Do not raise a generic error type. Do not catch a generic error type, except at the outermost boundary.
- `ERRORS-04` Catch the narrowest custom error type that the code can handle.
- `ERRORS-05` Put the context of the failure in typed fields of the error. Write a clear message that has no secret.
- `ERRORS-06` Convert an error from a library to a custom error type at the boundary. Keep the original error as the cause.
- `ERRORS-07` Do not swallow an error. Handle it, or let it propagate.
- `ERRORS-08` Add a test that raises each custom error type.

## Refactoring

- `REFACTOR-01` A refactor changes the structure and never the behavior.
- `REFACTOR-02` Separate a move from a change. One commit moves code. Another commit changes it.
- `REFACTOR-03` Keep the public interface: import paths, entry points, command options, and output. Mark a commit `refactor!:` when it changes the interface.
- `REFACTOR-04` Prove that the behavior is the same. The same tests pass. Edit a test only for an import path or a patch target, and name each edit in the pull request. Compare the output before and after (help text, screenshots, written files).
- `REFACTOR-05` Check that a comparison loads both versions. A comparison that loads the same code twice proves nothing.
- `REFACTOR-06` Work in small steps. Each commit builds and passes the tests. Use one pull request for each module or package.
- `REFACTOR-07` Do not mix a refactor and a feature. If the structure blocks a feature, refactor first.

## Do Not Assume

- `ASSUMPTIONS-01` Do not assume a naming convention for files or directories. Find them by content, and let the user register others.
- `ASSUMPTIONS-02` Do not hard-code the paths of one operating system. Use the platform library for the config, data, and cache directories. Support Linux, macOS, and Windows.
- `ASSUMPTIONS-03` Do not add a feature that no code reads. If a user questions the complexity, remove the feature.
- `ASSUMPTIONS-04` Do not assume how another tool works. Test it with a real run, for example with a fake local server, before you document it.
- `ASSUMPTIONS-05` When a project starts, list each choice of library or tool that this file does not name for the language of the project. Ask the user to research and decide each choice.
- `ASSUMPTIONS-06` Do not choose a library or a tool for the user. The user makes the decision.
- `ASSUMPTIONS-07` Do not start research on candidates unless the user asks. When the user asks, help with the research and leave the conclusion to the user.
- `ASSUMPTIONS-08` Record each decision of the user in a decision record.

## Security

- `SECURITY-01` Never print, log, or put a secret in an error message. Mask secrets on screen.
- `SECURITY-02` Never read a secret from a command argument. Use a hidden prompt or stdin.
- `SECURITY-03` Keep secret keys in a `.env` file. Do not put a secret in source code or in a tracked config file.
- `SECURITY-04` Add the `.env` file to the ignore list of the version control system (for example, `.gitignore`). Commit a `.env.example` file that has the key names and no values.
- `SECURITY-05` Write files that hold secrets atomically (temporary file, then rename) with owner-only permissions (for example, mode `0600`).
- `SECURITY-06` Send a request with a secret only to the host the user set. Do not follow redirects.
- `SECURITY-07` Read environment variables through a settings library. The library declares each setting with a type, validates it at start, and masks each secret on print. Do not read the environment directly in application code.
- `SECURITY-08` Use the secret type of the settings library for each secret setting. A secret value never appears in a log, a repr, or an error message.
- `SECURITY-09` Ask the user to choose the settings library for a language when the project starts (see "Do Not Assume"). A library that supports a `.env` file and a secrets directory is a good fit.

## User Interface

- `UI-01` Ask for confirmation before every destructive action. Name the item in the confirmation.
- `UI-02` Give every table pagination, sorting, filtering, and search. Keep the values of these four in the URL query parameters.
- `UI-03` Save the input of a form as the user types. Restore the input when the user returns to the page. Clear the saved input when the form submits.
- `UI-04` Do not save a secret field in the saved form input.
- `UI-05` Give every number input with a limited range a slider.
- `UI-06` Give every free-text input a clear option.

### Pure Components

- `PURITY-08` Write each component as a pure component by default. A pure component renders the same output for the same props and state.
- `PURITY-09` Pass all data to a component as props. Do not read hidden state during render (for example, a global variable, the clock, or a random source).
- `PURITY-10` Do not change props or shared state during render.
- `PURITY-11` Keep side effects out of render. Put them in event handlers or in the lifecycle hooks of the framework (for example, `useEffect` in React).
- `PURITY-12` Split a component into a presentational component and a container. The presentational component only renders. The container fetches data and holds state.
- `PURITY-13` Mark a component that has a side effect in its name or its doc comment.

## HTTP APIs

- `API-01` Limit the request rate for each client. Return status 429 with a `Retry-After` header when a client exceeds the limit.
- `API-02` Put a version in every API, in the URL path or in a header. Do not change a published version in a breaking way.
- `API-03` Add fields in a version. Do not remove or rename a field in the same version.
- `API-04` Return one error structure for all errors. Include a code, a message, and a request ID.
- `API-05` State the HTTP status code in the controller for each success path and each error path. Do not let a framework default choose the status code.
- `API-06` Paginate every list endpoint. Set a maximum page size.
- `API-07` Make PUT and DELETE idempotent. Accept an idempotency key for a POST that creates a resource.
- `API-08` Require authentication on every endpoint by default. Mark each public endpoint explicitly.
- `API-09` Check the permission of the caller on the server for every request.
- `API-10` Validate every request body and parameter at the boundary. Reject unknown input.
- `API-11` Set a timeout on every outgoing call. Set a size limit on every request.
- `API-12` Log each request with its request ID. Do not log a secret. Expose a health check endpoint.
- `API-13` Allow only listed origins for cross-origin requests. Do not use a wildcard for an authenticated endpoint.
- `API-14` Announce the removal of a version with a `Deprecation` header and a date. Keep the old version until that date.
- `API-15` Generate a machine-readable description of the API from the code (for example, an OpenAPI document). Check it in CI.

### Data and Dependencies

- `API-16` Make each database migration reversible. Do not mix a schema change with a data change in one migration.
- `API-17` Pin the version of each dependency. Scan the dependencies for known vulnerabilities in CI.

## Tests

- `TESTS-01` Write tests with the code. Run the full test suite before each commit.
- `TESTS-02` Isolate tests from the real home directory, the real environment, and the network. Use temporary directories, injected parameters, and mock transports.
- `TESTS-03` Add a test for each error path, not only for the success path.
- `TESTS-04` Check that CI passes before you merge.

## Delivery

- `DELIVERY-01` Split a rename or a refactor from a feature or a docs change. Use separate commits.
- `DELIVERY-02` Use `refactor!:` or a `BREAKING CHANGE:` footer when you remove or change a user-facing option.
- `DELIVERY-03` Give a command-line tool `--help` for the tool and for each command, with one example each.
- `DELIVERY-04` Give a tool a documented install method with a version option. Verify the checksum of the download.
- `DELIVERY-05` Do not merge a pull request unless the user says to merge. A request to merge one pull request does not cover the next one.
- `DELIVERY-06` After a network error on a write (merge, push), check the real state before you retry.
- `DELIVERY-07` After a merge, delete the branch locally and on the remote.

## Reporting

- `REPORTING-01` State what you tested and what you did not test.
- `REPORTING-02` State a known defect or limit, even when it is small.
- `REPORTING-03` When the user rejects a plan, change the plan file and ask again. Do not argue.

# Language-Specific Rules

## Python

- `PY-01` Mark optional and boolean parameters keyword-only with `*` in the definition, so a caller cannot pass them by position.
- `PY-02` Use absolute imports (`from package.module import name`).
- `PY-03` Do not use `Any`, `object` as a shortcut, or an untyped `dict` or `list`. Write the element types (`dict[str, int]`).
- `PY-04` Hint constants with `Final[str]`, class variables with `ClassVar[...]`, and type aliases with `TypeAlias`. Hint a local variable at its first assignment (`checks: list[Check] = []`).
- `PY-05` Check the types with `mypy --strict` (or an equal strict checker) in CI. Run `ruff check` with the `F`, `I`, and `ANN` rules in CI.
- `PY-06` Do not pin `python_version` in the checker config. Test on every Python version that CI runs.
- `PY-07` Use pydantic `BaseModel` classes for structured data. Do not pass plain dicts or dataclasses between functions.
- `PY-08` Use `polars` for data analysis. Do not use `pandas`. `polars` is faster.
- `PY-09` Use `platformdirs` for the config, data, and cache directories.
- `PY-10` Use `pydantic-settings` (`BaseSettings`) to read environment variables and the `.env` file. Declare each secret with `SecretStr`. Read a secret with `get_secret_value()` only at the point of use.
- `PY-11` Use `tmp_path` to isolate tests from the real home directory.

## TypeScript

- `TS-01` Take one options object and destructure it (`createUser({ name, role })`). Define its type with an `interface` or a `type`.
- `TS-02` Set `strict: true`. Do not use `any`.
