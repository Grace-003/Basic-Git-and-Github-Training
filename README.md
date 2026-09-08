# Git & GitHub — Complete Step by Step (VSCode + Terminal)

This training is split into 7 labs, each in its own README file. Work through them in order.

| Lab | Topic | File |
|---|---|---|
| Lab 1 | Initial Setup & First Commits (Steps 1–7) | [Lab1-Initial-Setup-First-Commits.md](Lab1-Initial-Setup-First-Commits.md) |
| Lab 2 | Undoing Changes (Steps 8–11) | [Lab2-Undoing-Changes.md](Lab2-Undoing-Changes.md) |
| Lab 3 | GitHub Basics (Steps 12–15) | [Lab3-GitHub-Basics.md](Lab3-GitHub-Basics.md) |
| Lab 4 | Branching & Merging (Steps 16–21) | [Lab4-Branching-Merging.md](Lab4-Branching-Merging.md) |
| Lab 5 | Advanced Commands (Steps 22–24) | [Lab5-Advanced-Commands.md](Lab5-Advanced-Commands.md) |
| Lab 6 | Tags & Releases (Steps 25–27) | [Lab6-Tags-Releases.md](Lab6-Tags-Releases.md) |
| Lab 7 | Inspection & Utilities (Step 28) | [Lab7-Inspection-Utilities.md](Lab7-Inspection-Utilities.md) |

Each lab README contains the exact terminal commands and VSCode actions needed to complete its steps, plus a **Use it when** note explaining the real situation each command is for.

## Quick lookup — "I want to..."

| Your situation | Command | Where |
|---|---|---|
| Start version control in a new folder | `git init` | [Lab 1](Lab1-Initial-Setup-First-Commits.md) |
| Save my work as a checkpoint | `git add .` + `git commit -m "..."` | [Lab 1](Lab1-Initial-Setup-First-Commits.md) |
| See what changed and who changed it | `git log`, `git diff`, `git blame` | [Lab 1](Lab1-Initial-Setup-First-Commits.md), [Lab 7](Lab7-Inspection-Utilities.md) |
| Throw away edits I haven't committed | `git restore <file>` | [Lab 2](Lab2-Undoing-Changes.md) |
| Undo a commit I already pushed | `git revert HEAD` | [Lab 2](Lab2-Undoing-Changes.md) |
| Redo my last commit (forgot a file / bad message) | `git reset --soft HEAD~1` | [Lab 2](Lab2-Undoing-Changes.md) |
| Delete my last commit and its changes entirely | `git reset --hard HEAD~1` | [Lab 2](Lab2-Undoing-Changes.md) |
| Put my local project on GitHub | `git remote add origin ...` + `git push -u origin main` | [Lab 3](Lab3-GitHub-Basics.md) |
| Get a copy of a project that's on GitHub | `git clone <url>` | [Lab 3](Lab3-GitHub-Basics.md) |
| Get my teammates' latest changes | `git pull origin main` | [Lab 3](Lab3-GitHub-Basics.md) |
| Stop being asked for a password every push | SSH key / Credential Manager | [Lab 3](Lab3-GitHub-Basics.md) |
| Work on a feature without breaking `main` | `git checkout -b feature/...` | [Lab 4](Lab4-Branching-Merging.md) |
| Bring a finished feature into `main` | `git merge <branch>` | [Lab 4](Lab4-Branching-Merging.md) |
| Fix a "CONFLICT" message | edit markers → `add` → `commit` | [Lab 4](Lab4-Branching-Merging.md) |
| Park unfinished work and switch tasks | `git stash` / `git stash pop` | [Lab 5](Lab5-Advanced-Commands.md) |
| Take just one commit from another branch | `git cherry-pick <hash>` | [Lab 5](Lab5-Advanced-Commands.md) |
| Update my branch with `main` and keep history linear | `git rebase main` | [Lab 5](Lab5-Advanced-Commands.md) |
| Mark a version like `v1.0.0` | `git tag -a v1.0.0 -m "..."` | [Lab 6](Lab6-Tags-Releases.md) |

> **Safety note:** `revert` and `merge` are safe on shared branches. `reset --hard` and `rebase` rewrite history — use them only on commits that exist nowhere but your own machine.
