# Lab 1 — Initial Setup & First Commits

[← Back to index](README.md)

## Step 1 — Configure Git (One Time Only)

Terminal:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@email.com"
git config --list
```

## Step 2 — Create Project & Initialize

Terminal:

```bash
mkdir my-project
cd my-project
git init
```

## Step 3 — Open in VSCode

File → Open Folder → select `my-project`

Then open terminal inside VSCode:

```
Ctrl + `
```

## Step 4 — First Commit

In VSCode — right click in Explorer panel → New File → name it `hello.txt`

Type inside `hello.txt`:

```
Hello Git
```

Save — `Ctrl + S`

Terminal:

```bash
git status
git add .
git commit -m "first commit"
```

## Step 5 — Second Commit

In VSCode — open `hello.txt`, add a new line:

```
Hello Git
I am learning Git
```

Save — `Ctrl + S`

Terminal:

```bash
git status
git add .
git commit -m "second commit"
```

## Step 6 — Third Commit

In VSCode — open `hello.txt`, add one more line:

```
Hello Git
I am learning Git
Git is a version control system
```

Save — `Ctrl + S`

Terminal:

```bash
git status
git add .
git commit -m "third commit"
```

## Step 7 — View History

Terminal:

```bash
git log
git log --oneline
git log --oneline --graph --all
```

---
Next: [Lab 2 — Undoing Changes](Lab2-Undoing-Changes.md)
