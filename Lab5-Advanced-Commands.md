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

### Rebase in everyday use — `git pull --rebase` vs `git pull --no-rebase`

> **Use it when:** you committed something locally, a teammate pushed something to GitHub, and now `git pull` has two histories to combine. These two flags are the two ways of combining them — merge, or rebase.

Starting point for both examples — the common history is `A --- B`, then the two sides go their own way:

```
Local:      A --- B --- C        (your commit C)
GitHub:     A --- B --- D        (teammate's commit D)
```

#### Option 1 — merge (`--no-rebase`)

```bash
git pull origin main --no-rebase
```

Git joins the two histories by creating a **new merge commit** `M`:

```
A --- B --- C -------- M
       \              /
        ------ D -----
```

`M` = merge commit. Your `C` and their `D` both stay exactly as they were — nothing is rewritten. The history keeps a visible record that two lines of work came together here.

- **Good:** nothing is rewritten, so it's always safe — even on a branch other people share.
- **Cost:** the graph branches and rejoins. On a busy repo you get a lot of "Merge branch 'main'..." commits.

#### Option 2 — rebase (`--rebase`)

```bash
git pull origin main --rebase
```

Git takes your local commit `C` off first, so you're temporarily back to the remote's history:

```
A --- B --- D
```

Then it re-applies `C` on top of the latest remote commit:

```
A --- B --- D --- C'
```

Notice: **`C` ≠ `C'`**. It has the same changes and the same message, but a different parent, so it's technically a **new commit with a new hash** — the old `C` is gone.

Result:

```
A --- B --- D --- C'
```

The history is one straight line, with no merge commit — the same thing `git rebase main` did above, just done as part of the pull.

- **Good:** clean, linear log — easy to read and to `git bisect`.
- **Cost:** it rewrites your commits. Fine for commits that only exist on your machine; the golden rule above still applies — **never rebase commits you've already pushed and shared**, because everyone else still has the old hashes.

#### Which one should you use?

| Situation | Use |
|---|---|
| Your local commits aren't pushed yet | `--rebase` — keeps history linear |
| You're on a shared branch others have already pulled from | `--no-rebase` — safe, rewrites nothing |
| You're not sure | `--no-rebase` — merging is never wrong, just noisier |

> **Tip:** if you never want to think about it again, set a default once per machine:
>
> ```bash
> git config --global pull.rebase false   # always merge
> git config --global pull.rebase true    # always rebase
> ```
>
> Without this, newer Git versions refuse to pull when both sides have moved and print a hint asking you to pick one — that's the message this section explains.

---
Next: [Lab 6 — Tags & Releases](Lab6-Tags-Releases.md)
