# Lab 5 — Advanced Commands

[← Back to index](README.md)

## Step 22 — Stash

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
