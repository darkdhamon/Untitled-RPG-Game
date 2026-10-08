# Repository Workflow

## Branches

- `main`: latest released code; pull requests only after initial repository bootstrap.
- `dev`: base for ongoing development.
- Feature branches: `codex/<issue#>-<issuetitle>`, created from `dev`.

Protect `main` and `dev` against deletion and force pushes. Require resolved review conversations. Changes to `main` require a pull request.

## Issues and planning board

Board lanes: Backlog, Ready, In Progress, In Review, Done, Released.

New issues start in Backlog. Ready requires clear requirements, acceptance criteria, resolved blockers, and a Fibonacci size estimate (1, 2, 3, 5, 8, 13, or 21); at most eight issues belong in Ready.

Use priorities Critical, High, Normal, and Low, with Normal as the default. Record a blocked issue's previous lane and return it to Backlog with a `blocked` label.

Implementation begins only after an issue leaves Backlog, unless the user explicitly overrides this. Move the issue to In Progress when its feature branch is created, In Review when its ready-for-review PR is opened, Done when merged into `dev` with all criteria met, and Released when merged into `main`. Feature PRs address issues; they do not close them.

Documentation-only work may bypass the issue-driven workflow. Initial repository setup establishes the branches before protections are enabled.

## Reviews and validation

All available tests must pass for PRs into either long-lived branch. Main requires at least 70% coverage of testable application code; dev warns below 70%. Exclude test projects from coverage.

There is no application code or test runner yet. Add the actual build, test, coverage workflow, and required status checks when the engine and toolchain are selected, before application changes are merged. Do not claim coverage from documentation checks or use placeholder passing tests.

The Codex Connector bot is the automated reviewer. Request `@codex review` if automatic review has not started. Establish a five-minute review heartbeat when a task enters In Review, following the universal instructions. Review signals, comments, checks, and unresolved threads must be checked before any merge. A bot review comment requires user guidance before completing a PR.

Default recurring project automations are created only when requested.

## Commit convention

For issue work:

```text
Codex - Issue #{issue number} - {Title}

{Summary of changes}
```

For documentation-only bootstrap work without an issue, use a descriptive `Codex - ...` commit title.
