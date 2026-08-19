# Lab 3 — GitHub Basics

[← Back to index](README.md)

## Step 12 — Connect to GitHub

Go to GitHub.com → New Repository → name it `my-project` → Create (no README)

Terminal:

```bash
git remote add origin https://github.com/username/my-project.git
git remote -v
```

## Step 13 — Push to GitHub

Terminal:

```bash
git push -u origin main
```

Refresh GitHub in browser — your files are live ✅

## Step 14 — Clone a Repo

Terminal:

```bash
cd Desktop
git clone https://github.com/username/my-project.git
cd my-project
```

In VSCode:

```
File → Open Folder → select cloned my-project
```

## Step 15 — Pull Changes from GitHub

In VSCode — open `hello.txt`, add a line:

```
Hello Git
I am learning Git
Git is a version control system
this line added by teammate
```

Save — `Ctrl + S`

Terminal:

```bash
git add .
git commit -m "teammate added a line"
git push origin main
```

Now on the original machine:

```bash
git pull origin main
```

Open `hello.txt` in VSCode — teammate's line is now here ✅

---
Next: [Lab 4 — Branching & Merging](Lab4-Branching-Merging.md)
