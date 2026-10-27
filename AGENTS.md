# AGENTS.md

Guidance for AI coding agents working on the Varbase AI Default recipe.

## Before you start

Read the project history and context first:

- **Documentation** lives on the Varbase docs site: [Varbase AI Recipes](https://docs.varbase.vardot.com/developers/understanding-varbase/varbase-ai-recipes). Keep `README.md` short and link there; add no `docs/` folder.
- **`CHANGELOG.md`**: what changed in each release, newest first. Read it before
  proposing changes so you follow the established direction and versioning.
- **Merge request comments and history** on
  [git.drupalcode.org/project/varbase_ai_default](https://git.drupalcode.org/project/varbase_ai_default/-/merge_requests):
  the reasoning behind recent changes lives in the MR discussions.
- **Issue comments** on
  [drupal.org/project/issues/varbase_ai_default](https://www.drupal.org/project/issues/varbase_ai_default):
  the Problem/Motivation and Proposed resolution for each change.

## When you make a change

- Add an entry under `## [Unreleased]` in `CHANGELOG.md`.
- Keep commit messages in the Drupal commit-type format:
  `{type}: #{issueID} Summary` (see https://www.drupal.org/node/3586390).
- Never bump the version or tag a release without explicit maintainer approval.
- This recipe requires no packages: Varbase AI Base requires it and every recipe it applies.
- This is a `drupal-recipe`; keep configuration in the recipe, not in
  `config/install` or `config/optional`.
