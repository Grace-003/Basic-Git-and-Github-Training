# Lab 5 — Advanced Commands

[← Back to index](README.md)

## Step 22 — Stash

> **Use it when:** you're mid-way through something, it's not commit-ready, and you suddenly need a clean working directory — an urgent bug to fix, a branch to switch to, a `git pull` that won't run while you have local changes.
> **Real example:** you're building a feature, your boss says production is broken. `git stash` → fix the bug → `git stash pop` → you're back exactly where you left off.
> **`pop` vs `apply`:** `pop` restores the work and removes it from the stash list; `apply` restores it but keeps a copy stashed.

In VSCode — open `hello.txt`, add a line but DO NOT commit:

```
Hello from main branch
I am learning Git
Git is a version control system
this is incomplete work
```

Save — `Ctrl + S`

Terminal:

```bash
git stash                           # work saved, file cleaned
git status                          # nothing to commit ✅
```

Open `hello.txt` in VSCode — incomplete line is gone ✅

```bash
git stash list                      # see your stash
git stash pop                       # bring work back
```

Open `hello.txt` in VSCode — incomplete line is back ✅

## Step 23 — Cherry Pick

> **Use it when:** you want *one specific commit* from another branch, not the whole branch. Merge brings everything; cherry-pick brings one thing.
> **Real example:** you fixed a critical bug on your feature branch, but that branch also has half-finished work that isn't ready to ship. Cherry-pick just the bug-fix commit onto `main` and release it — the unfinished work stays behind.

Terminal:

```bash
git checkout -b hotfix
```

In VSCode — right click → New File → `bugfix.txt`

Type:

```
critical bug is fixed here
```

Save — `Ctrl + S`

Terminal:

```bash
git add .
git commit -m "critical bug fix"
git log --oneline                   # copy the commit hash e.g. a1b2c3d

git checkout main
git cherry-pick a1b2c3d             # apply only that one commit
ls                                  # bugfix.txt is here ✅
```

## Step 24 — Rebase

> **Use it when:** your feature branch is behind `main` and you want a clean, straight history instead of a merge commit. Rebase lifts your commits off and replays them on top of the latest `main`, as if you'd started work today.
> **Rebase vs merge:** merge preserves exactly what happened (with a merge commit); rebase rewrites your commits for a tidier log. Many teams rebase their own feature branch before opening a PR.
> **The golden rule:** never rebase a branch you've already pushed and others are using — it rewrites history and breaks their copies. Rebase your own local branches only.

Terminal:

```bash
git checkout -b feature/rebase-demo
```

In VSCode — right click → New File → `rebase.txt`

Type:

```
this file is on feature branch
```

Save — `Ctrl + S`

Terminal:

```bash
git add .
git commit -m "feature rebase commit"

git rebase main                     # replay on top of main
git checkout main
git merge feature/rebase-demo       # fast forward, clean history
git log --oneline --graph           # linear, no merge commit ✅
```

---
Next: [Lab 6 — Tags & Releases](Lab6-Tags-Releases.md)
