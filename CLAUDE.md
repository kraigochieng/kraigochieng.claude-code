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

## Answers

- `COMMUNICATION-01` Put the answer or the recommendation first. Put the reasons after it.
- `COMMUNICATION-02` Answer a small question, or describe work of one step, in a few sentences. Use a design document for all other work (`DESIGN-01`).

## Tables and Diagrams

- `COMMUNICATION-03` Use a table for a list in which each item has more than one attribute.
- `COMMUNICATION-04` Use a diagram for a system that has more than two parts.
- `COMMUNICATION-05` Do not put a list of steps in a table. Use a numbered list.

## Status

- `COMMUNICATION-06` Give each check a status: run and passed, run and failed, not run, or owner action. Do not write "done" for a check that you did not run.

# Planning Pattern

## Design Document

- `DESIGN-01` Choose the tier of the design document from the size of the work:

| Tier | Size of the work | Content |
|---|---|---|
| Small | One step | No document. Answer in a few sentences. |
| Medium | One pull request with two or more commits | Sections 1, 2, 3, 8, 11, and 12 of `DESIGN-02`. |
| Large | More than one pull request, or a change that is hard to reverse | All sections of `DESIGN-02`. |

- `DESIGN-02` A large plan for a feature, a fix, or a refactor has these sections, in this order:

1. Header table: issue, status, dependencies, decisions from the owner.
2. Context: the problem and what prompted the work.
3. Goals and non-goals, in two columns.
4. Current state and proposed state, each with a diagram.
5. Contracts and examples: the signature and an example table for each unit (`CONTRACT-01` to `CONTRACT-04`).
6. Design decisions: a table with decision, choice, and reason.
7. Alternatives considered: a table with option and reason for rejection.
8. Work breakdown: a table with pull request, commit, commit type, and check.
9. Risks: a table with risk, effect, and mitigation.
10. Rollout: numbered steps. Mark the steps that only the owner can do.
11. Verification: a table with check, command, and status.
12. Open questions.

## Contracts and Examples

- `CONTRACT-01` Before you write code, state the contract of each planned unit: the one-sentence responsibility (`STRUCTURE-03`), the name, the type of each parameter, and the return type.
- `CONTRACT-02` Show the behavior of each unit in an example table: the input on the left and the expected output on the right. Include each error path.
- `CONTRACT-03` Give each example row one test. Write the rows in the same order as the commits.
- `CONTRACT-04` Keep each table to about 10 rows. Split a longer table by case group.

## Decision Record

- `DECISION-01` Write one decision record for each decision that is hard to reverse and for each decision of the user (`ASSUMPTIONS-07`). A decision record has three parts: context, decision, and consequences.

# Modeling Pattern

## State Machines

- `STATE-01` Explain a process that has states and events (for example an invite, an order, or a job) as a state machine. Do not explain it as a story.
- `STATE-02` Name every state and every event. Mark the start state and the end states.
- `STATE-03` Show the transitions in a table with the columns from-state, event, to-state, and action. Add a diagram when the process has more than two states.
- `STATE-04` Show each decision in a table: the conditions on the left and the result on the right. Include the refusal cases, with the reason the user sees.
- `STATE-05` Check three things before you finish: each state has a way out or is an end state, each event is handled in each state, and an event that changes nothing is shown as refused or ignored.

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
- `CONVENTIONS-14` Write every name in full words. Do not use a short form of a word (for example, `index`, not `idx`; `message`, not `msg`). Do not use a single-letter name, not even for a loop target, a lambda parameter, or a query alias.

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
- `STRUCTURE-10` Do not nest loops. Do not nest `if` statements. Use an early return or a guard clause, a combined condition, or a separate function with its own name. Prefer an operation over a whole collection (for example, `map`, `filter`, or a set-based query) to a loop.
- `STRUCTURE-11` When you design a feature that has states, write the states and transitions first (`STATE-02`, `STATE-03`). Then write the decision as one pure function over the states, and test each row of the decision table (`STATE-04`).

## Pure Functions

- `PURITY-01` Write each function as a pure function by default. A pure function returns the same output for the same input and has no side effect.
- `PURITY-02` Pass every value that a function needs as a parameter. Do not read hidden state (for example, a global variable, the clock, the environment, or a random source).
- `PURITY-03` Do not change a parameter or any shared state. Return a new value.
- `PURITY-04` Keep side effects (input and output, storage, network, time, randomness) in a thin outer layer. Pass their results into the pure functions.
- `PURITY-05` Inject a side-effect dependency (for example, a clock or a transport) as a parameter when a function must use one.
- `PURITY-06` Test a pure function with input and expected output. It needs no mock.
- `PURITY-07` Mark a function or a component that has a side effect in its name or its doc comment, so that a reader can see it.

## Data Access

- `DATA-01` Put all data access in a repository. The repository owns the queries and the storage calls. Do not read or write the data store outside a repository.
- `DATA-02` Give the repository a typed interface. Return the structured types of the project, not raw rows.
- `DATA-03` Make each database migration reversible. Do not mix a schema change with a data change in one migration.

## Layers

- `LAYERS-01` Split a service that handles requests into three layers: controller, service, and repository.
- `LAYERS-02` Let the controller own transport behavior only. It parses and validates the request, calls one service, and maps the result to a response. Do not put a business rule or a data access call in a controller.
- `LAYERS-03` Let the service own business behavior only. It takes typed input and returns a typed result. Do not let a service use transport concepts (for example, a request object, a response object, a status code, or a header).
- `LAYERS-04` Raise a domain error in the service. Map the domain error to a transport status in the controller.
- `LAYERS-05` Let dependencies point one way: controller to service, and service to repository. A lower layer does not import from a higher layer.
- `LAYERS-06` Test a service without a transport. Test a controller with a fake service.

## Errors

- `ERRORS-01` Define a custom error type for each failure that the project expects. Name the type for the failure (for example, `UserNotFoundError`). Derive every custom error type from one base error type of the project.
- `ERRORS-02` Do not raise a generic error type. Do not catch a generic error type, except at the outermost boundary. Catch the narrowest custom error type that the code can handle.
- `ERRORS-03` Put the context of the failure in typed fields of the error. Write a clear message that has no secret.
- `ERRORS-04` Convert an error from a library to a custom error type at the boundary. Keep the original error as the cause.
- `ERRORS-05` Do not swallow an error. Handle it, or let it propagate.

## Refactoring

- `REFACTOR-01` A refactor changes the structure and never the behavior.
- `REFACTOR-02` Separate a move from a change. One commit moves code. Another commit changes it.
- `REFACTOR-03` Keep the public interface: import paths, entry points, command options, and output. Mark a commit `refactor!:` when it changes the interface.
- `REFACTOR-04` Prove that the behavior is the same. The same tests pass. Edit a test only for an import path or a patch target, and name each edit in the pull request. Compare the output before and after (help text, screenshots, written files).
- `REFACTOR-05` Check that a comparison loads both versions. A comparison that loads the same code twice proves nothing.
- `REFACTOR-06` Work in small steps. Use one pull request for each module or package.
- `REFACTOR-07` Do not mix a refactor, a rename, a feature, or a docs change in one commit. If the structure blocks a feature, refactor first.

## Do Not Assume

- `ASSUMPTIONS-01` Do not assume a naming convention for files or directories. Find them by content, and let the user register others.
- `ASSUMPTIONS-02` Do not hard-code the paths of one operating system. Use the platform library for the config, data, and cache directories. Support Linux, macOS, and Windows.
- `ASSUMPTIONS-03` Do not add a feature that no code reads. If a user questions the complexity, remove the feature.
- `ASSUMPTIONS-04` Do not assume how another tool works. Test it with a real run, for example with a fake local server, before you document it.
- `ASSUMPTIONS-05` When a project starts, list each library or tool choice that this file does not name for the language of the project. Ask the user to research and decide each choice. Do not choose for the user.
- `ASSUMPTIONS-06` Do not start research on candidates unless the user asks. When the user asks, help with the research and leave the conclusion to the user.
- `ASSUMPTIONS-07` Record each decision of the user in a decision record (`DECISION-01`).
- `ASSUMPTIONS-08` Before you add or upgrade a dependency, ask the user to approve it. Name the package, the version, the reason, and whether it is runtime or dev. Install nothing before the user says yes.

## Security

- `SECURITY-01` Never print, log, or put a secret in an error message or a repr. Mask secrets on screen.
- `SECURITY-02` Never read a secret from a command argument. Use a hidden prompt or stdin.
- `SECURITY-03` Keep secret keys in a `.env` file. Do not put a secret in source code or in a tracked config file. Add the `.env` file to the ignore list of the version control system (for example, `.gitignore`). Commit a `.env.example` file that has the key names and no values.
- `SECURITY-04` Write files that hold secrets atomically (temporary file, then rename) with owner-only permissions (for example, mode `0600`).
- `SECURITY-05` Send a request with a secret only to the host the user set. Do not follow redirects.
- `SECURITY-06` Read environment variables through a settings library that the user chooses (see `ASSUMPTIONS-05`). The library types each setting, validates it at start, and masks each secret on print. Use its secret type for each secret setting. Do not read the environment directly in application code. A library that supports a `.env` file and a secrets directory is a good fit.

## User Interface

- `UI-01` Ask for confirmation before every destructive action. Name the item in the confirmation.
- `UI-02` Give every table pagination, sorting, filtering, and search. Keep the values of these four in the URL query parameters.
- `UI-03` Save the input of a form as the user types. Restore the input when the user returns to the page. Clear the saved input when the form submits. Do not save a secret field.
- `UI-04` Give every number input with a limited range a slider.
- `UI-05` Give every free-text input a clear option.

### Pure Components

- `PURITY-08` Write each component as a pure component by default. A pure component renders the same output for the same props and state. Pass all data as props. Do not read hidden state, and do not change props or shared state, during render.
- `PURITY-09` Keep side effects out of render. Put them in event handlers or in the lifecycle hooks of the framework (for example, `useEffect` in React).
- `PURITY-10` Split a component into a presentational component and a container. The presentational component only renders. The container fetches data and holds state.

## HTTP APIs

- `API-01` Limit the request rate for each client. Return status 429 with a `Retry-After` header when a client exceeds the limit.
- `API-02` Put a version in every API, in the URL path or in a header. Do not change a published version in a breaking way. Add fields in a version. Do not remove or rename a field in the same version.
- `API-03` Return one error structure for all errors. Include a code, a message, and a request ID.
- `API-04` State the HTTP status code in the controller for each success path and each error path. Do not let a framework default choose the status code.
- `API-05` Paginate every list endpoint. Set a maximum page size.
- `API-06` Make PUT and DELETE idempotent. Accept an idempotency key for a POST that creates a resource.
- `API-07` Require authentication on every endpoint by default. Mark each public endpoint explicitly.
- `API-08` Check the permission of the caller on the server for every request.
- `API-09` Validate every request body and parameter at the boundary. Reject unknown input.
- `API-10` Set a timeout on every outgoing call. Set a size limit on every request.
- `API-11` Log each request with its request ID. Expose a health check endpoint.
- `API-12` Allow only listed origins for cross-origin requests. Do not use a wildcard for an authenticated endpoint.
- `API-13` Announce the removal of a version with a `Deprecation` header and a date. Keep the old version until that date.
- `API-14` Generate a machine-readable description of the API from the code (for example, an OpenAPI document). Check it in CI.

## Tests

- `TESTS-01` Write tests with the code. Run the full test suite before each commit.
- `TESTS-02` Isolate tests from the real home directory, the real environment, and the network. Use temporary directories, injected parameters, and mock transports.
- `TESTS-03` Add a test for each error path, not only for the success path. Include a test that raises each custom error type.
- `TESTS-04` Check that CI passes before you merge.

## Delivery

- `DELIVERY-01` Give a command-line tool `--help` for the tool and for each command, with one example each.
- `DELIVERY-02` Give a tool a documented install method with a version option. Verify the checksum of the download.
- `DELIVERY-03` After a network error on a write (merge, push), check the real state before you retry.
- `DELIVERY-04` Pin the version of each dependency. Scan the dependencies for known vulnerabilities in CI.

## Diligence

- `DILIGENCE-01` Take the time that the task needs. Do not rush to give an answer.
- `DILIGENCE-02` Before you write or suggest code, read the code that the change touches. Check each fact that the answer depends on.
- `DILIGENCE-03` Before you give a result, check it against the request. Run the tests that cover the change.

## Reporting

- `REPORTING-01` State what you tested and what you did not test.
- `REPORTING-02` State a known defect or limit, even when it is small.
- `REPORTING-03` When the user rejects a plan, change the plan file and ask again. Do not argue.
- `REPORTING-04` State each limit that affects the result. This covers reports and every code suggestion, library choice, or design recommendation. A limit is a tool you cannot use, a step you skip, an input you cannot verify, a version or behavior you did not test, or a doubt about your answer. State it with the suggestion, before the user relies on it.

# Language-Specific Rules

## Python

- `PY-01` Mark optional and boolean parameters keyword-only with `*` in the definition, so that a caller cannot pass them by position.
- `PY-02` Use absolute imports (`from package.module import name`).
- `PY-03` Do not use `Any`, `object` as a shortcut, or an untyped `dict` or `list`. Write the element types (`dict[str, int]`).
- `PY-04` Hint constants with `Final[str]`, class variables with `ClassVar[...]`, and type aliases with `TypeAlias`. Hint a local variable at its first assignment (`checks: list[Check] = []`).
- `PY-05` Check the types with `mypy --strict` (or an equal strict checker) in CI. Run `ruff check` with the `F`, `I`, and `ANN` rules in CI.
- `PY-06` Do not pin `python_version` in the checker config. Test on every Python version that CI runs.
- `PY-07` Use pydantic `BaseModel` classes for structured data. Do not pass plain dicts or dataclasses between functions.
- `PY-08` Use `polars` for data analysis. Do not use `pandas`.
- `PY-09` Use `platformdirs` for the config, data, and cache directories.
- `PY-10` Use `pydantic-settings` (`BaseSettings`) to read environment variables and the `.env` file. Declare each secret with `SecretStr`. Read a secret with `get_secret_value()` only at the point of use.
- `PY-11` Use `tmp_path` to isolate tests from the real home directory.

## TypeScript

- `TS-01` Take one options object and destructure it (`createUser({ name, role })`). Define its type with an `interface` or a `type`.
- `TS-02` Set `strict: true`. Do not use `any`.

## SQL

- `SQL-01` Do not give a table an alias. Write the full table name in every reference (for example, `stories.story_id`, not `s.story_id`).
- `SQL-02` When one query reads the same table twice, give each reference an alias. The alias holds the full table name and the role of the reference (for example, `stories_as_duplicate_target`). Do not use a short alias.
- `SQL-03` Name every variable, parameter, and column in full words (rule `CONVENTIONS-14`).
