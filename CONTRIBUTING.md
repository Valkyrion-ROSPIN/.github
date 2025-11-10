# Contributing to Valkyrion

## 0. Quick Start (TL;DR)

1. Make sure your idea is covered by an existing issue or create one that explains the value and scope.
2. Fork the repository (or create a feature branch if you already have write access).
3. Clone your fork locally, add the `upstream` remote, and stay synced with `main`.
4. Create a focused branch such as `feature/workshop-outline` or `docs/faq-update`.
5. Edit files, stage changes, and commit in small, reviewable chunks.
6. Rebase your branch on top of the latest `upstream/main` before pushing.
7. Push to your fork, open a pull request (PR), complete the checklist, and link the issue.
8. Address review feedback promptly and keep rebasing until the PR is ready to merge.

Use the remainder of the document as a Git learning path and reference.

## 1. Getting Ready (No Git Background? Start Here)

### 1.1 Accounts & Tools

1. **Create a GitHub account:** <https://github.com/signup>
2. **Install Git:**
   - Windows: [Git for Windows](https://git-scm.com/download/win) (enable Git Bash during install).
   - macOS: run `xcode-select --install` or use [Homebrew](https://brew.sh/) with `brew install git`.
   - Linux: install via your package manager, e.g., `sudo apt install git`.
3. **Optional helpers:** GitHub Desktop, VS Code, or any editor with Markdown preview.
4. **Communication:** use GitHub Issues/Discussions and the workshop chat for quick questions.

### 1.2 Configure Git Once

Replace the placeholders with your info:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
```

Authenticate with GitHub using HTTPS + a personal access token or via SSH keys (`ssh-keygen -t ed25519 -C "you@example.com"`). The [GitHub docs](https://docs.github.com/authentication) have detailed walkthroughs.

### 1.3 Local Workspace Basics

Each Valkyrion-ROSPIN repository may contain documentation, code, data pipelines, or a mix of all three. Read that repo’s `README.md` for language/runtime requirements, dependency managers, or tooling tips, then install only what it calls for.

### 1.4 Staying in Touch

Leave progress updates on your issue or PR, and note when you pause work so someone else can pick it up. Collaboration is easier when everyone knows the current state.

## 2. Repository Structure

Every project lives under `https://github.com/Valkyrion-ROSPIN/<repo-name>`. Replace `<repo-name>` with the actual repository you want to work on (e.g., `satellite-data-kit`). Most repositories include:

- `README.md` — overview, setup instructions, and project goals.
- `CONTRIBUTING.md` — either this shared guide or a repo-specific addendum.
- Source folders (e.g., `src`, `notebooks`, `docs`, `infra`) with their own READMEs when needed.
- Supporting files such as `.github/`, `LICENSE`, or workflow definitions.

Whenever you add a new top-level directory, update that repo’s `README.md` so others can discover it quickly.

## 3. Git Workflow in Depth

### 3.1 Forking (if you do not have direct push access)

1. Click **Fork** on GitHub.
2. Keep the default settings and create the fork under your account.
3. You now have `https://github.com/YOURUSER/<repo-name>`.

If you are already a maintainer, you can skip the fork and work directly in the main repository—but still create feature branches.

### 3.2 Cloning & Remotes

Clone your fork and add the original repository as `upstream`:

```bash
git clone https://github.com/YOURUSER/<repo-name>.git
cd <repo-name>
git remote add upstream https://github.com/Valkyrion-ROSPIN/<repo-name>.git
git remote -v   # verify origin (your fork) and upstream (main repo)
```

Replace `<repo-name>` with the repository you are contributing to.

### 3.3 Branch Naming & Scope

- Base every change on top of `main`.
- Use short, specific names such as `docs/add-schedule`, `fix/spelling`, or `ops/update-board`.
- Keep each branch focused on one logical change. If scope creeps, split it into multiple branches/PRs.

### 3.4 Making Changes Locally

```bash
git checkout -b docs/improve-onboarding
# edit files in your editor
git status       # see what changed
git diff         # review unstaged edits
git add CONTRIBUTING.md README.md
```

Use `git add -p` to stage piece by piece when you want a very clean history.

### 3.5 Crafting Commits

- Commit early and often; each commit should answer “why did we do this?”
- Prefer [Conventional Commits](https://www.conventionalcommits.org/) (e.g., `docs: explain fork workflow`) but plain language is acceptable if it is descriptive.
- Multi-line commit example:

  ```
  docs: expand git workflow section

  - add forking/cloning instructions
  - describe rebasing before PR
  - clarify how to resolve conflicts
  ```

### 3.6 Stay Current by Rebasing

Before pushing or opening a PR, fast-forward your branch onto the latest `main`:

```bash
git checkout main
git fetch upstream
git rebase upstream/main
git checkout docs/improve-onboarding
git rebase main
```

Rebasing keeps history linear and reduces merge conflicts. If you already pushed the branch, force-push with care:

```bash
git push --force-with-lease origin docs/improve-onboarding
```

`--force-with-lease` ensures you do not overwrite someone else’s work accidentally.

### 3.7 Resolving Merge Conflicts

When Git reports conflicts:

1. Open each conflicted file and look for the markers `<<<<<<<`, `=======`, `>>>>>>>`.
2. Decide which lines to keep or combine, then delete the markers.
3. Stage the file (`git add path/to/file`).
4. Continue the rebase (`git rebase --continue`) or complete the merge if you were merging.
5. Rerun any checks (spellcheck, markdown preview, etc.).

If you are unsure, paste the conflict chunk into the issue/PR and ask for help.

### 3.8 Push Your Branch

```bash
git push -u origin docs/improve-onboarding
```

The `-u` flag remembers the upstream tracking branch so future pushes only need `git push`.

## 4. Writing and Submitting a Pull Request

### 4.1 Pre-flight Checklist

- Confirm the branch addresses only the linked issue.
- Proofread Markdown and confirm links/images work.
- Run whatever checks make sense for your change (spellcheck, Markdown preview, or custom scripts if/when they exist).
- Rebase onto the latest `upstream/main`.
- Squash or reorganize commits only if it improves clarity.

### 4.2 Drafting the PR Description

A solid PR template usually covers:

- **Context:** what problem does this solve?
- **Changes:** bullet list of key edits.
- **Testing/verification:** how you confirmed the change works (screenshots, commands, manual checks).
- **Follow-up work:** anything intentionally out of scope.

Always link the issue (`Closes #123` or `Related to #123`) so it closes automatically when merged.

### 4.3 Open the PR

1. Visit your fork on GitHub and press **Compare & pull request** (or use `gh pr create`).
2. Target `Valkyrion-ROSPIN/<repo-name>` → `main`.
3. Fill out the description, add labels if you can, and request reviewers (`@Valkyrion` maintainers if unsure).
4. Use “Draft PR” if you want feedback before finishing.

## 5. Reviews, Updates, and Merging

### 5.1 During Review

- Expect at least one maintainer review.
- Respond politely to every comment (“Fixed in 123abc”, “Clarified”, or explain why you prefer a different approach).
- Keep discussions public in the PR so others learn from the context.

### 5.2 Updating After Feedback

- Make the requested changes locally.
- Rebase on top of the latest `upstream/main`.
- Force-push with `--force-with-lease` so the PR reflects the new history.
- Leave a comment that summarizes what changed since the last review round.

### 5.3 How PRs Get Merged

- Maintainers typically **squash merge** so the main branch stays clean.
- If preserving individual commits matters (e.g., splitting docs vs assets), mention that in the PR.
- Before merging, maintainers double-check that:
  - The PR description is complete.
  - The linked issue is accurate.
  - Required reviews have been given.
  - Checks (if any) have passed.

If a PR goes stale, maintainers may close it after a polite ping; you can always reopen when ready.

## 6. Maintainer Responsibilities

- Triage issues, label them for newcomers, and keep backlog priorities visible.
- Review PRs promptly with actionable feedback.
- Help contributors learn Git by pointing to relevant sections of this guide.
- Keep `main` clean and deployable; revert breaking changes quickly.
- Update onboarding docs whenever workflows or tools change.

## 7. Troubleshooting & FAQ

| Problem | Fix |
| --- | --- |
| `permission denied` when pushing | You used SSH but did not add your key to GitHub. Upload it in **Settings → SSH and GPG keys**. |
| `fatal: remote origin already exists` | Remove or rename the old remote before adding a new one (`git remote remove origin`). |
| “I can’t push because of non-fast-forward” | Rebase onto `upstream/main`, then push with `--force-with-lease`. |
| PR shows other people’s commits | Your branch is outdated; run `git fetch upstream && git rebase upstream/main`. |
| Unsure where to start | Filter issues by `good first issue`, or ask for pairing/mentoring in Discussions. |

If your question is missing, open an issue labeled `question` so we can expand this table.

## 8. Recognition & Next Steps

- We thank contributors in release notes and workshop updates. Add yourself to a future `AUTHORS.md` once it exists.
- Join demo or planning calls to showcase your work and help direct future efforts.
- Frequent contributors can request additional permissions (triage, maintainer) to keep things moving.

Your enthusiasm keeps Valkyrion moving forward—thanks for lending your time and curiosity! 🚀
