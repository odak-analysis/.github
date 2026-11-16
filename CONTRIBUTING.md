# Contributing to ODAK

This guide is the team agreement for branches, commits and pull requests. It applies to every repository of the `odak-analysis` organization. It follows the course Handbook (Version Control and Integration Guidelines, Branch Naming, GitHub Flow) and the SE 4910 Guidelines.

Why it matters: the course validates each student's work through **branch naming, commit history and Jira issue association**. Work on a branch that is not linked to a Jira issue is graded **0**, and a commit without proper naming is treated as **no commit**.

## 1. Start from a Jira issue

Every change belongs to a Jira issue in project `ODK`. If there is no issue for your work, ask the Team Leader to create one before you start.

When you start working on the issue, move it to **In Progress** in Jira.

## 2. Branches

Create one branch per Jira issue from the latest `main`:

```
git checkout main
git pull
git checkout -b task/ODK-<n>
```

The prefix matches the Jira issue type:

| Jira issue type | Branch name     |
|-----------------|-----------------|
| Story           | `story/ODK-<n>` |
| Task            | `task/ODK-<n>`  |
| Bug             | `bug/ODK-<n>`   |

Write the key exactly as Jira shows it: uppercase `ODK`, a hyphen, the number.

## 3. Commits

Commit messages follow [Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/). The Jira key is the scope, so Jira links every commit to its issue.

```
<type>(ODK-<n>): <description>

[optional body]

[optional footer]
```

**Rules**

1. `ODK-<n>` is the key of the issue your branch belongs to, in uppercase.
2. `<description>` is in English, in the imperative mood ("add", not "added" or "adds"), starts with a lowercase letter and has no full stop at the end.
3. Keep the first line to about 72 characters. Use the body to explain *why* when the change is not obvious.
4. One commit = one logical change. Do not mix unrelated changes in one commit.

**Types**

| Type       | Use for                                                 |
|------------|---------------------------------------------------------|
| `feat`     | A new feature for the user                              |
| `fix`      | A bug fix                                               |
| `docs`     | Documentation only (proposal, reports, README)          |
| `style`    | Formatting only, no change in behaviour                 |
| `refactor` | Code change that neither fixes a bug nor adds a feature |
| `perf`     | Performance improvement                                 |
| `test`     | Adding or correcting tests                              |
| `build`    | Build system or dependencies                            |
| `ci`       | Continuous integration configuration                    |
| `chore`    | Other maintenance (repository setup, configuration)     |
| `revert`   | Reverting an earlier commit                             |

**Examples**

```
docs(ODK-26): rewrite README for ODAK
feat(ODK-41): add entry counting line
fix(ODK-52): handle dropped camera frames
```

A change that breaks existing behaviour adds `!` after the scope and a footer:

```
feat(ODK-60)!: change aggregate message format

BREAKING CHANGE: the edge module now sends timestamps as ISO 8601 strings.
```

## 4. Pull requests

1. Push your branch and open a Pull Request into `main`.
2. Title: `ODK-<n>: <short summary>`, e.g. `ODK-11: Set up repository`.
3. Add a teammate in the **Reviewers** field of the pull request. Move the Jira issue to **Review**. The Team Leader watches how reviews are distributed and may change the reviewer.
4. The review takes place in the pull request discussion. The author answers every comment and pushes fixes to the same branch.
5. If the reviewer requests changes, the author moves the Jira issue back to **In Progress**, pushes the fixes and moves it to **Review** again.
6. After the reviewer approves, the **Team Leader** merges the pull request and moves the Jira issue to **Done**.

**Merging**

- Never push directly to `main`.
- Use **Create a merge commit**. Do not squash or rebase, because that rewrites the commit history that is used for grading.
- Do not delete the branch after merging; the branch and its history are evidence of the work.
- `main` is protected: a pull request with at least one approval is required, and only merge commits are allowed.

## 5. Reviewing

1. Open the pull request, go to **Files changed** and comment on the lines you want to discuss.
2. Check the change against the Definition of Done in the Jira issue.
3. Start each comment with a label:
   - `[blocking]` must be fixed before merging
   - `[suggestion]` optional improvement
   - `[question]` you need an explanation
4. Finish with **Review changes** → **Approve** or **Request changes**.
5. Approve only when every `[blocking]` comment is resolved.

## 6. Keeping Jira and GitHub in sync

Jira shows branches, commits and pull requests automatically when they contain the issue key (`ODK-<n>`). Statuses and descriptions are updated by hand.

**Statuses — update immediately**

| When…                                                  | Move the Jira issue to |
|--------------------------------------------------------|------------------------|
| you start working on the issue                         | **In Progress**        |
| you open a pull request and add a reviewer             | **Review**             |
| the reviewer requests changes                          | **In Progress**        |
| you have pushed the fixes                              | **Review**             |
| the Team Leader merges the pull request                | **Done**               |

**Descriptions — update together, not after every small change**

If the scope of your work changes (extra files, settings or steps), update the Jira description (What to do + Definition of Done) and the pull request description in one go — at the latest before you ask for a review.

## 7. Documents

Project documents are written and reviewed on Confluence. The versions that were submitted for the course are kept in the [`odak-docs`](https://github.com/odak-analysis/odak-docs) repository.

## How Jira links your work

Jira's GitHub integration finds the issue key in:

| Where                  | Example                                          |
|------------------------|--------------------------------------------------|
| Branch name            | `task/ODK-11`                                    |
| Commit message         | `chore(ODK-11): add .gitignore`                  |
| Pull request title     | `ODK-11: Set up repository`                      |

If the key is missing or misspelled (e.g. `odk-11`, `ODK11`), the work does not appear on the Jira issue.
