# GitHub Workflow Reference

This repository is an interactive **GitHub Skills** exercise that guides new contributors through the fundamental concepts of GitHub.  The automation is powered entirely by GitHub Actions workflows located in `.github/workflows/`.  Although the repository does not expose traditional source‐code APIs, the individual workflows _are_ public automation components that can be inspected, reused, or adapted in other projects.

This document provides a complete reference for every public workflow shipped with this exercise.

> **Tip**  
> All workflows are intentionally **disabled by default** (except `0-start-exercise.yml`).  The exercise enables the next workflow automatically as you progress through each step.

---

## Table of Contents

| Step | Workflow file | Purpose |
|------|---------------|---------|
| 0 | `0-start-exercise.yml` | Kick-off the exercise, open the guidance issue, and enable **Step 1**. |
| 1 | `1-create-a-branch.yml` | Validate that you created the branch `my-first-branch`; then enable **Step 2**. |
| 2 | `2-commit-a-file.yml` | Check that you committed `PROFILE.md` to `my-first-branch`; then enable **Step 3**. |
| 3 | `3-open-a-pull-request.yml` | Verify that you opened a pull request from `my-first-branch` to `main`; then enable **Step 4**. |
| 4 | `4-merge-your-pull-request.yml` | Detect that the pull request was successfully merged and finish the exercise. |

---

## 0 – Start Exercise  (`.github/workflows/0-start-exercise.yml`)

|                 | Details |
|-----------------|---------|
| **Trigger**     | `push` to `main` (usually the first commit that copies the exercise template) |
| **Permissions** | `contents: write`, `actions: write`, `issues: write` |
| **Jobs**        |
| `start_exercise` | Composite action `skills/exercise-toolkit@v0.6.0` that opens the **exercise issue** and captures its URL. |
| `post_next_step_content` | Posts the "Step 1" instructions as an issue comment and enables the workflow named **"Step 1"**. |

### Usage example

You rarely run this workflow manually.  It executes automatically when the repository is created from the template.  If you ever need to re-run it, push any commit to `main`:

```bash
git checkout main
touch rebuild && git add rebuild && git commit -m "rerun: start exercise" && git push
```


---

## 1 – Create a Branch  (`.github/workflows/1-create-a-branch.yml`)

|                 | Details |
|-----------------|---------|
| **Trigger**     | `push` to branch `my-first-branch` |
| **Permissions** | `contents: read`, `actions: write`, `issues: write` |
| **Environment** | `STEP_2_FILE=".github/steps/2-commit-a-file.md"` |
| **Jobs**        |
| `find_exercise` | Locates the main exercise issue. |
| `check_step_work` | Posts a _"checking work"_ comment, ensures branch name matches exactly, then posts completion feedback. |
| `post_next_step_content` | Adds **Step 2** instructions, disables this workflow, and enables **"Step 2"**. |

### How to trigger

```bash
# Inside your fork of the repository
# 1️⃣ create the branch exactly as requested
git checkout -b my-first-branch
git push -u origin my-first-branch  # 👈 triggers the workflow
```


---

## 2 – Commit a File  (`.github/workflows/2-commit-a-file.yml`)

|                 | Details |
|-----------------|---------|
| **Trigger**     | `push` to branch `my-first-branch` |
| **Permissions** | `contents: read`, `actions: write`, `issues: write` |
| **Environment** | `STEP_3_FILE=".github/steps/3-open-a-pull-request.md"` |
| **Jobs**        |
| `find_exercise` | Finds the exercise issue. |
| `check_step_work` | Confirms that `PROFILE.md` exists in the commit. |
| `post_next_step_content` | Adds **Step 3** instructions, disables this workflow, and enables **"Step 3"**. |

### How to trigger

```bash
git checkout my-first-branch
# create the profile readme
echo "# My GitHub Profile" > PROFILE.md
git add PROFILE.md
git commit -m "Add PROFILE.md"
git push               # 👈 triggers the workflow
```


---

## 3 – Open a Pull Request  (`.github/workflows/3-open-a-pull-request.yml`)

|                 | Details |
|-----------------|---------|
| **Trigger**     | `pull_request` targeting `main` on events `opened`, `synchronize`, `reopened`, or `edited` |
| **Permissions** | `contents: read`, `actions: write`, `issues: write` |
| **Environment** | `STEP_4_FILE=".github/steps/4-merge-your-pull-request.md"` |
| **Jobs**        |
| `find_exercise` | Locates the exercise issue. |
| `check_step_work` | Validates PR title is exactly **"Add my first file"** and non-empty description, provides feedback table. |
| `post_step_4_content` | Publishes **Step 4** instructions, disables this workflow, and enables **"Step 4"**. |

### How to trigger

Open a pull request from `my-first-branch` into `main`:

```bash
# Using the GitHub CLI
gh pr create --title "Add my first file" --body "Adds PROFILE.md via the Introduction to GitHub course" --base main --head my-first-branch
```


---

## 4 – Merge Your Pull Request  (`.github/workflows/4-merge-your-pull-request.yml`)

|                 | Details |
|-----------------|---------|
| **Trigger**     | `pull_request` `closed` event where the PR was **merged** into `main` |
| **Permissions** | `contents: write`, `actions: write`, `issues: write` |
| **Environment** | `REVIEW_FILE=".github/steps/x-review.md"` |
| **Jobs**        |
| `find_exercise` | Finds the exercise issue. |
| `check_step_work` | Confirms the PR met merge requirements and was indeed merged. |
| `post_review_content` | Adds the course review comment. |
| `finish_exercise` | Runs `skills/exercise-toolkit/.github/workflows/finish-exercise.yml` to close out the lesson. |
| `disable_workflow` | Disables itself so it won’t run again. |

### How to trigger

After the checks are green, click **Merge pull request** in the web UI or:

```bash
# With GitHub CLI
gh pr merge --merge --delete-branch
```


---

## Reusing these workflows in another project

If you’d like to incorporate these learning steps into your own repository, copy the desired workflow file(s) from `.github/workflows/` and adjust:

1. **Branch names** – e.g. change `my-first-branch` to match your convention.
2. **File paths** – update `PROFILE.md` or step markdown paths.
3. **Exercise messages** – modify the strings under `intro-message`, `template-file`, or inline `echo` commands.

Because each workflow is fully declarative YAML, you do **not** need to publish them as reusable workflows.  They can live directly in your repo.

---

## Frequently Asked Questions

### The workflow didn’t run — what went wrong?

| Possible cause | Fix |
|----------------|-----|
| You used a branch name other than `my-first-branch`. | Rename or recreate the branch with the exact name. |
| The pull-request title does not match **“Add my first file”**. | Edit the title in the PR to the expected value. |
| You disabled a workflow early. | Re-enable it under **Actions → … → Enable workflow** or push a new commit to retrigger. |

### Can I run the course again from scratch?

1. Delete the repository (or create a fresh fork from the template).  
2. Push a commit to `main` to re-activate `0-start-exercise.yml`.

---

_This documentation was generated automatically via Cursor_ 🪄✨