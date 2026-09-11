# Git Flow Cheatsheet

Simple guide for a 5-person team using Git Flow branching.

## Branch Types

| Branch | Purpose | Created From | Merges Into |
| --- | --- | --- | --- |
| `main` | Always production-ready code | - | - |
| `develop` | Latest integrated work-in-progress | `main` | `main` (via release) |
| `feature/*` | New feature or task | `develop` | `develop` |
| `release/*` | Prepare a new production release | `develop` | `main` and `develop` |
| `hotfix/*` | Urgent fix for production | `main` | `main` and `develop` |

## Common Commands

| Command | What It Does |
| --- | --- |
| `git clone <url>` | Download a copy of the repo to your machine |
| `git status` | Show changed/staged files |
| `git branch` | List local branches |
| `git checkout develop` | Switch to the `develop` branch |
| `git checkout -b feature/login develop` | Create and switch to a new feature branch from `develop` |
| `git add .` | Stage all changed files |
| `git commit -m "message"` | Save staged changes with a message |
| `git push origin feature/login` | Upload your branch to the remote repo |
| `git pull origin develop` | Fetch and merge latest `develop` changes into your branch |
| `git fetch` | Download remote changes without merging |
| `git merge feature/login` | Merge a branch into your current branch |
| `git fetch origin && git rebase origin/develop` | Reapply your commits on top of the latest remote `develop` (cleaner history) |
| `git log --oneline --graph` | View commit history as a compact graph |
| `git branch -d feature/login` | Delete a branch after it's merged |
| `git tag v1.0.0` | Mark a specific commit as a release version |
| `git stash` | Temporarily save uncommitted changes |
| `git stash pop` | Restore stashed changes |
| `git diff` | Show unstaged changes |
| `git reset --soft HEAD~1` | Undo last commit but keep changes staged |

## Typical Team Workflow

| Step | Command |
| --- | --- |
| 1. Start a feature | `git checkout -b feature/xyz develop` |
| 2. Work + commit | `git add .` then `git commit -m "..."` |
| 3. Keep up to date | `git pull origin develop` (or rebase) |
| 4. Push for review | `git push origin feature/xyz` |
| 5. Open PR/MR | `feature/xyz` → `develop` |
| 6. After approval, merge | Merge PR, then delete `feature/xyz` |
| 7. Release time | Create `release/1.0` from `develop`, test, merge into `main` and `develop`, tag it |
| 8. Emergency fix | Create `hotfix/x` from `main`, fix, merge into `main` and `develop`, tag it |

## Quick Tips for Teams

- Never commit directly to `main` or `develop` — always use a feature branch.
- Keep feature branches small and short-lived.
- Pull/rebase from `develop` often to avoid big merge conflicts.
- Use pull requests for code review before merging.
