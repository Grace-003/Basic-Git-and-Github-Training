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

## SSH Authentication Setup for GitHub

HTTPS asks for a username/password (or token) every time you push. SSH uses a key pair instead — set it up once per machine.

### Windows — use HTTPS 

On Windows, authenticate over HTTPS using **Git Credential Manager (GCM)** — it comes bundled with Git for Windows and is the default/recommended way to sign in.

```powershell
# 1. Clone (or set an existing repo's remote) using the HTTPS URL
git clone https://github.com/username/my-project.git
```

```powershell
# or, for a repo you already have locally:
git remote set-url origin https://github.com/username/my-project.git
git remote -v
```

The first time you `push`/`pull`/`clone`, a browser window pops up asking you to log in to GitHub — sign in once and Git Credential Manager caches it for every future command, no key generation needed.

> **Fallback (only if GCM's browser popup doesn't appear):** GitHub no longer accepts your account password over HTTPS, so generate a **Personal Access Token** and use it as the password instead:
> ```
> GitHub.com → profile picture → Settings → Developer settings
> → Personal access tokens → Tokens (classic) → Generate new token
> → check "repo" scope → Generate → copy the token
> ```
> Where to put it — a terminal/Git prompt appears (in PowerShell, or a small Git popup window) asking for:
> ```
> Username for 'https://github.com': your-github-username
> Password for 'https://your-github-username@github.com': <paste the token here>
> ```
> Type your GitHub username as usual, and paste the **token** in place of the password (right-click to paste in PowerShell, since Ctrl+V may not work). It's cached after the first use, so you won't be asked again on that machine.

### macOS (Terminal)

```bash
# 1. Check for an existing key
ls -al ~/.ssh

# 2. Generate a new key
ssh-keygen -t ed25519 -C "your_email@example.com"

# 3. Start the ssh-agent
eval "$(ssh-agent -s)"

# 4. (Recommended) create/update ~/.ssh/config to auto-load the key from Keychain
cat >> ~/.ssh/config << 'EOF'
Host github.com
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519
EOF

# 5. Add the key to the agent and Keychain
ssh-add --apple-use-keychain ~/.ssh/id_ed25519

# 6. Copy the public key
pbcopy < ~/.ssh/id_ed25519.pub
```

### Linux (Terminal)

```bash
# 1. Check for an existing key
ls -al ~/.ssh

# 2. Generate a new key
ssh-keygen -t ed25519 -C "your_email@example.com"

# 3. Start the ssh-agent
eval "$(ssh-agent -s)"

# 4. Add the key to the agent
ssh-add ~/.ssh/id_ed25519

# 5. Copy the public key (install xclip if needed: sudo apt install xclip)
xclip -sel clip < ~/.ssh/id_ed25519.pub

# or just print it and copy manually
cat ~/.ssh/id_ed25519.pub
```

### Add the key to GitHub (macOS & Linux)

```
GitHub.com → click profile picture → Settings
→ SSH and GPG keys → New SSH key
→ Title: e.g. "My Laptop" → Key: paste (Ctrl+V) → Add SSH key
```

### Test the connection (macOS & Linux)

```bash
ssh -T git@github.com
```

Type `yes` if asked to trust the host. You should see:

```
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

### Switch a repo from HTTPS to SSH (macOS & Linux)

```bash
git remote set-url origin git@github.com:username/my-project.git
git remote -v
```

Now `git push` / `git pull` will use SSH — no more username/password prompts ✅

---
Next: [Lab 4 — Branching & Merging](Lab4-Branching-Merging.md)
