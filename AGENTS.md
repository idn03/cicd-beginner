# Instructions for Codex

## Project context

This repository is a beginner-first, hands-on guide to CI/CD. The learner wants to understand where to start, how to write and explain scripts for TypeScript and SQL projects, how GitHub Rulesets protect branches, how to organize a repository, and what to consider when deploying.

The README is the current project overview and learning roadmap. At the start of this repository, there is no application stack, database, package manager, or hosting provider selected. Do not assume one without grounding it in the user's request or repository contents.

## How to work in this repository

- Teach through small, reviewable steps. Explain the purpose of each script, workflow, and important setting in Vietnamese, including how to run it locally and interpret failures.
- Prefer working local commands first, then automate the same checks in GitHub Actions.
- When adding a tool or platform, explain why it fits and what alternatives affect; do not add dependencies or workflows merely to make the repository look complete.
- Keep example configuration safe: least-privilege workflow permissions, no secrets in source or logs, and no production data in tests.
- Explain that GitHub Rulesets are configured in GitHub settings, while workflows and scripts live in the repository. Include practical steps and note any account/permission-dependent options.
- Introduce deployment only after the app, target platform, credentials model, and rollback approach are understood. Prefer staging before production.
- Keep the README and learning docs aligned with the repository's actual state. Label proposed structure and examples as such until implemented.
- Avoid unexplained jargon. Define terms when they first matter, and show expected commands/results for a beginner.

## Suggested progression

1. Choose or create a minimal sample app and identify its runtime and package manager.
2. Add scripts for typecheck, lint, formatting, tests, and build; document each one.
3. Run those checks in a pull request workflow and explain its triggers, jobs, permissions, dependency installation, and logs.
4. Document and configure an appropriate GitHub Ruleset, including required status checks and bypass considerations.
5. Add SQL tooling and isolated database checks once the database/framework is selected.
6. Add build artifacts and a controlled staging/production deployment path once hosting is selected.
