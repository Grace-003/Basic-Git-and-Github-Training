# Git & GitHub — Beginner's Guide

This guide explains what Git and GitHub are, how to create and clone repositories, and the basic Git commands every beginner should know. Follow the steps in order.

## What is Git?
- Git is a distributed version control system. It tracks changes to files, lets you work on versions (commits), and supports branching and merging.

## What is GitHub?
- GitHub is a web-based hosting service for Git repositories. It provides remote storage, collaboration features (pull requests, issues), and a web UI.

## Before you start (setup)
1. Install Git:

   - Windows: download from https://git-scm.com/download/win
   - macOS: `brew install git` or https://git-scm.com/download/mac
   - Linux: use your distro package manager, e.g. `sudo apt install git`

2. Configure Git (one-time):

```
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

3. Create a GitHub account at https://github.com if you want to use remote repositories.

## Create a new repository on GitHub (basic)
1. Log in to GitHub.
2. Click **New repository** (green button) or go to https://github.com/new.
3. Enter a repository name, optional description, choose Public/Private, and click **Create repository**.

## Clone a repository (copy from GitHub to your machine)
1. On the repository page, click **Code** and copy the HTTPS URL (or SSH if you prefer).
2. In your terminal run:

```
git clone https://github.com/username/repo-name.git
```

This creates a folder `repo-name` with the repository files.

## Create a local repository and push it to GitHub
1. Create a local project folder and initialize Git:

```
mkdir my-project
cd my-project
git init
```

2. Add a file and make the first commit:

```
echo "# My Project" > README.md
git add README.md
git commit -m "Initial commit"
```

3. Connect to GitHub (replace URL with the repo you created on GitHub):

```
git remote add origin https://github.com/username/repo-name.git
git branch -M main
git push -u origin main
```

## Basic Git commands (common workflow)
- `git status` : see changed/untracked files
- `git add <file>` : stage changes for commit
- `git commit -m "message"` : record staged changes
- `git log` : view commit history
- `git diff` : see unstaged changes
- `git rm <file>` : remove a file
- `git mv <old> <new>` : rename/move file
- `git pull` : fetch + merge remote changes
- `git push` : send commits to remote

Typical sequence while working:

```
git pull           # update local branch
# edit files
git add .
git commit -m "describe changes"
git push
```

## Branching (work on features safely)
- Create and switch to a branch:

```
git checkout -b feature-branch
```

or with newer Git:

```
git switch -c feature-branch
```

- Push branch to remote and set upstream:

```
git push -u origin feature-branch
```

Branches let you work on changes without affecting `main` (or `master`).

## Merging (bring branches together)

Local merge:

```
git checkout main
git pull
git merge feature-branch
git push
```

Merging on GitHub (recommended for collaboration):
1. Push your branch to GitHub.
2. On the repository page, click **Compare & pull request** for your branch.
3. Review changes, add a description, and click **Create pull request**.
4. After review, click **Merge pull request** → **Confirm merge**.

## When do merge conflicts occur?
- A merge conflict happens when the same lines in the same file were changed differently in two branches and Git cannot automatically decide which change to keep.

Common scenarios:
- Both you and someone else edited the same line in a file on different branches.
- A file was deleted on one branch and modified on the other.

## How to resolve merge conflicts (step-by-step)
1. Try to merge or pull and Git reports conflicts.

2. Open the conflicted files. You will see markers:

```
<<<<<<< HEAD
your changes
=======
their changes
>>>>>>> branch-name
```

3. Edit the file to keep the correct content. Remove the conflict markers and make it the final version you want.

4. Stage the resolved files and commit:

```
git add <resolved-file>
git commit -m "Resolve merge conflict in <file>"
git push
```

If you were resolving a pull request, pushing the commit to the branch updates the PR and allows merging.

GUI tools to help resolve conflicts:
- VS Code Source Control view highlights conflicts and provides actions.
- GitHub web editor sometimes allows simple conflict resolution.
- GitHub Desktop and other clients provide visual merge tools.

## Safe updating: fetch, rebase, or merge
- Before you start working, update your branch to avoid conflicts:

```
git fetch origin
git rebase origin/main
```

or

```
git pull --rebase
```

Rebasing keeps a cleaner history; merging keeps the original commit graph. Learn both and choose a team policy.

## Quick cheat-sheet (commands)
```
# Setup
git config --global user.name "Name"
git config --global user.email "you@example.com"

# Clone
git clone <repo-url>

# Create branch
git checkout -b my-branch

# Stage + commit
git add .
git commit -m "message"

# Push
git push origin my-branch

# Merge into main locally
git checkout main
git merge my-branch
git push

# Resolve conflicts: edit files, then
git add <file>
git commit
git push
```

## Tips for beginners
- Commit often with clear messages.
- Pull before you push to reduce conflicts.
- Use branches for features/fixes.
- Use descriptive branch names: `feature/login`, `fix/typo`.
- Read PR diffs before merging.

## Further reading
- Official Git docs: https://git-scm.com/doc
- GitHub Guides: https://guides.github.com

---
