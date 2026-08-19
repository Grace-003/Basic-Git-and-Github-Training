# Lab 4 — Branching & Merging

[← Back to index](README.md)

## Step 16 — Create a Branch

Terminal:

```bash
git branch                          # see current branches
git checkout -b feature/login       # create and switch
git branch                          # confirm you are on new branch
```

## Step 17 — Work on Branch & Commit

In VSCode — right click → New File → `login.txt`

Type inside `login.txt`:

```
This is the login page
```

Save — `Ctrl + S`

Terminal:

```bash
git add .
git commit -m "add login page"
```

## Step 18 — Merge Branch into Main

Terminal:

```bash
git checkout main
ls                              # login.txt not here
git merge feature/login
ls                              # login.txt is here now ✅
git log --oneline --graph --all
```

## Step 19 — Create a Merge Conflict

Terminal:

```bash
git checkout -b feature/conflict
```

In VSCode — open `hello.txt`, change first line to:

```
Hello from feature branch
I am learning Git
Git is a version control system
```

Save — `Ctrl + S`

Terminal:

```bash
git add .
git commit -m "feature branch change"
git checkout main
```

In VSCode — open `hello.txt`, change first line to:

```
Hello from main branch
I am learning Git
Git is a version control system
```

Save — `Ctrl + S`

Terminal:

```bash
git add .
git commit -m "main branch change"
git merge feature/conflict          # conflict will appear
```

## Step 20 — Resolve the Conflict

In VSCode — open `hello.txt`, you will see:

```
<<<<<<< HEAD
Hello from main branch
=======
Hello from feature branch
>>>>>>> feature/conflict
```

Delete the conflict markers, keep what you want:

```
Hello from main branch
I am learning Git
Git is a version control system
```

Save — `Ctrl + S`

Terminal:

```bash
git add .
git commit -m "conflict resolved"
git log --oneline --graph --all
```

## Step 21 — Delete a Branch

Terminal:

```bash
git branch -d feature/login         # safe delete
git branch -d feature/conflict      # safe delete
git branch                          # confirm deleted ✅
```

---
Next: [Lab 5 — Advanced Commands](Lab5-Advanced-Commands.md)
