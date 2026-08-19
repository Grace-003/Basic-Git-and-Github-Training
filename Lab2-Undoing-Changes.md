# Lab 2 — Undoing Changes

[← Back to index](README.md)

## Step 8 — Discard Unsaved Changes (restore)

In VSCode — open `hello.txt`, add a bad line:

```
Hello Git
I am learning Git
Git is a version control system
this is a mistake
```

Save — `Ctrl + S`

Terminal — discard that change:

```bash
git restore hello.txt
```

Now open `hello.txt` in VSCode — the bad line is gone ✅

## Step 9 — Undo Last Commit (revert)

In VSCode — open `hello.txt`, add a line:

```
Hello Git
I am learning Git
Git is a version control system
this line should not have been committed
```

Save — `Ctrl + S`

Terminal:

```bash
git add .
git commit -m "bad commit"
git log --oneline         # see bad commit at top
git revert HEAD           # creates a new undo commit
git log --oneline         # bad commit still there but neutralized
```

## Step 10 — Reset Soft (reset --soft)

In VSCode — open `hello.txt`, add a line:

```
Hello Git
I am learning Git
Git is a version control system
accidental line
```

Save — `Ctrl + S`

Terminal:

```bash
git add .
git commit -m "accidental commit"
git log --oneline             # see it at top

git reset --soft HEAD~1       # commit gone, changes still staged
git status                    # file still green (staged)
git log --oneline             # commit is gone ✅
```

## Step 11 — Reset Hard (reset --hard)

In VSCode — open `hello.txt`, add a line:

```
Hello Git
I am learning Git
Git is a version control system
delete everything including this
```

Save — `Ctrl + S`

Terminal:

```bash
git add .
git commit -m "commit to destroy"
git log --oneline

git reset --hard HEAD~1       # commit gone + file changes gone
git log --oneline             # commit removed ✅
```

Open `hello.txt` in VSCode — the line is completely gone ✅

---
Next: [Lab 3 — GitHub Basics](Lab3-GitHub-Basics.md)
