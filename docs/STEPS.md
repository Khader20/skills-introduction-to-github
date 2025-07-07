# Course Step Reference

The **Introduction to GitHub** exercise walks learners through four incremental lessons, each delivered via an issue comment that points to a Markdown file under `.github/steps/`.

This document summarizes each lesson, its learning objectives, and the hands-on activity required for completion.

| Step | File | Core topic | Hands-on activity |
|------|------|------------|-------------------|
| 1 | `1-create-a-branch.md` | Branches | Create a branch named **`my-first-branch`** off `main`. |
| 2 | `2-commit-a-file.md` | Commits | Add a new file **`PROFILE.md`** to the branch and commit it with message `Add PROFILE.md`. |
| 3 | `3-open-a-pull-request.md` | Pull Requests | Open a pull request from `my-first-branch` into `main` titled **“Add my first file”** and supply a description. |
| 4 | `4-merge-your-pull-request.md` | Merging | Merge the pull request and delete the branch. |
| Final Review | `x-review.md` | Wrap-up | Provides a recap and next-steps resources. |

---

## 1. Create a Branch (`.github/steps/1-create-a-branch.md`)

**Learning objectives**

* Understand what a branch is and why it is useful.
* Learn how to create a branch in the GitHub web UI.

**Usage example**

```bash
# Create the branch locally and push it
git checkout -b my-first-branch
# 👇 Push triggers Step-1 workflow validation
git push -u origin my-first-branch
```

---

## 2. Commit a File (`.github/steps/2-commit-a-file.md`)

**Learning objectives**

* Understand commits and commit messages.
* Practice adding a Markdown file via the GitHub web editor.

**Usage example**

```bash
# Still on my-first-branch
echo "Welcome to my GitHub profile!" > PROFILE.md
git add PROFILE.md
git commit -m "Add PROFILE.md"
git push     # 👈 Workflow validates the commit
```

---

## 3. Open a Pull Request (`.github/steps/3-open-a-pull-request.md`)

**Learning objectives**

* Grasp the concept of pull requests for collaboration.
* Learn how to compare branches and request feedback.

**Usage example (GitHub CLI)**

```bash
gh pr create \
  --base main \
  --head my-first-branch \
  --title "Add my first file" \
  --body "Adds PROFILE.md via the Introduction to GitHub course"
```

---

## 4. Merge Your Pull Request (`.github/steps/4-merge-your-pull-request.md`)

**Learning objectives**

* Understand the merge process and what it does to project history.
* Practice using the GitHub UI to merge and delete a feature branch.

**Usage example (CLI)**

```bash
gh pr merge --merge --delete-branch
```

---

## Final Review (`.github/steps/x-review.md`)

Summarizes the learner’s achievements and points to additional resources such as further GitHub Skills courses and the Student Developer Pack.

---

### Reusing the Lesson Content

Copy any of the step Markdown files into your own repository and adjust the instructions to match your workflow. Because the files are ordinary Markdown, they can be embedded in READMEs, wikis, or issue templates.