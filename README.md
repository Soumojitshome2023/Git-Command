# 🚀 Git Commands Cheat Sheet

A comprehensive, organized, and user-friendly collection of commonly used Git commands to streamline your workflow.

---

## 📑 Table of Contents

- [🛠️ Setup & Configuration](#setup-configuration)
- [👤 User Identity & Authentication](#user-identity-authentication)
- [📝 Basic Workflow](#basic-workflow)
- [🌿 Branching & Merging](#branching-merging)
- [📦 Stashing & Cleaning](#stashing-cleaning)
- [🔍 Inspection & Comparison](#inspection-comparison)
- [🚨 Undo & Recover (The "Panic" Section)](#undo-recover-panic-section)
- [🚀 Remote Repository Management](#remote-repository-management)
- [🛠️ Advanced Operations](#advanced-operations)

---

<a id="setup-configuration"></a>
## 🛠️ Setup & Configuration

| Command | Description |
| :--- | :--- |
| `git init` | Initialize a local Git repository in the current directory. |
| `git clone <url>` | Create a local copy of a remote repository. |
| `git remote add origin <url>` | Connect your local repository to a remote server. |
| `git remote -v` | List all remote connections and their URLs. |
| `git remote get-url origin` | Show the URL for the 'origin' remote. |
| `git remote set-url origin <url>` | Change the remote repository URL (e.g., switch to SSH). |

---

<a id="user-identity-authentication"></a>
## 👤 User Identity & Authentication

| Command | Description |
| :--- | :--- |
| `git config --list` | Show all current Git configuration (including user info). |
| `git config user.name` | View the current configured user name. |
| `git config user.email` | View the current configured email ID. |
| `git config --global user.name "Name"` | Set/Change your global user name. |
| `git config --global user.email "email"` | Set/Change your global email ID. |
| `git config --global --unset user.name` | Remove the global user name configuration. |

### 🔐 Authentication & "Logout"
Git doesn't have a direct `logout` command. Access is managed via your OS Credential Manager or SSH keys.

- **To "Logout" (Clear saved credentials on Windows):**
  - Open **Credential Manager** > **Windows Credentials**.
  - Find `git:https://github.com` and click **Remove**.
- **To Switch Accounts:**
  - Update your local/global config: `git config --global user.name "NewUser"`.
  - Next time you push, Git will prompt for new credentials if they were cleared.

### 🔑 Connecting via SSH
1. **Check for existing keys:** `ls -al ~/.ssh`
2. **Generate new key:** `ssh-keygen -t ed25519 -C "your_email@example.com"`
3. **Add key to SSH Agent:** `eval "$(ssh-agent -s)"` followed by `ssh-add ~/.ssh/id_ed25519`
4. **Test connection:** `ssh -T git@github.com`

---


<a id="basic-workflow"></a>
## 📝 Basic Workflow

| Command | Description |
| :--- | :--- |
| `git status` | Show the status of changes as untracked, modified, or staged. |
| `git add <file>` | Add a specific file to the staging area. |
| `git add .` | Add all new and changed files to the staging area. |
| `git commit -m "[message]"` | Commit staged changes with a descriptive message. |
| `git push origin <branch>` | Push local branch commits to the remote repository. |
| `git pull` | Update your local repository with the latest changes from remote. |
| `git pull origin <branch>` | Pull changes from a specific remote branch. |

---

<a id="branching-merging"></a>
## 🌿 Branching & Merging

| Command | Description |
| :--- | :--- |
| `git branch` | List local branches (asterisk indicates current branch). |
| `git branch -a` | List all branches (local and remote). |
| `git branch <branch-name>` | Create a new branch. |
| `git checkout <branch-name>` | Switch to a different branch. |
| `git checkout -b <branch-name>` | Create a new branch and switch to it immediately. |
| `git checkout -b <name> origin/<name>` | Clone a remote branch and switch to it. |
| `git branch -d <branch-name>` | Delete a local branch (must be merged first). |
| `git branch -D <branch-name>` | Force delete a local branch. |
| `git merge <branch-name>` | Merge the specified branch into the current one. |
| `git checkout -` | Switch to the branch last checked out. |

---

<a id="stashing-cleaning"></a>
## 📦 Stashing & Cleaning

| Command | Description |
| :--- | :--- |
| `git stash` | Temporarily store all modified tracked files. |
| `git stash list` | List all stashed changes. |
| `git stash pop` | Restore the most recently stashed files and remove them from stash. |
| `git stash apply` | Restore stashed files without removing them from stash. |
| `git stash clear` | Remove all stashed entries. |
| `git rm -r <file>` | Remove a file (or folder) and stage the deletion. |
| `git rm -r --cached <file>` | Remove a file from version control but keep it locally. |

---

<a id="inspection-comparison"></a>
## 🔍 Inspection & Comparison

| Command | Description |
| :--- | :--- |
| `git log` | Show the commit history for the current branch. |
| `git log --oneline` | Show commit history in a condensed, one-line format. |
| `git log --summary` | View changes with detailed statistics (files changed, etc.). |
| `git diff <source> <target>` | Preview changes between two branches before merging. |
| `git diff --staged` | Show differences between the staging area and the last commit. |

---

<a id="undo-recover-panic-section"></a>
## 🚨 Undo & Recover (The "Panic" Section)

| Command | Description |
| :--- | :--- |
| `git reset <file>` | Unstage a file, keeping the changes in the working directory. |
| `git checkout -- <file>` | Discard changes to a specific file (restore from last commit). |
| `git commit --amend` | Replace the last commit with a new one (useful for fixing message/files). |
| `git reset --hard <commit-hash>` | **WARNING:** Reset everything to a specific commit. All local changes will be lost. |
| `git push -f origin <branch>` | **WARNING:** Force push changes to remote (use with caution). |

### 🛠️ Restore Working Directory to a Specific Commit
To replace all files with the state from a specific commit without moving the branch pointer:
```bash
git checkout <branch-name>
git checkout <commit-hash> -- .
git add .
git commit -m "Revert code to commit <commit-hash>"
git push origin <branch-name>
```

---

<a id="remote-repository-management"></a>
## 🚀 Remote Repository Management

| Command | Description |
| :--- | :--- |
| `git remote set-url origin <url>` | Change the remote repository URL (e.g., switch to SSH). |
| `git push -u origin <branch>` | Push and set the remote as the default upstream. |
| `git push origin --delete <branch>` | Delete a branch from the remote repository. |
| `git remote prune origin` | Remove local references to deleted remote branches. |

---

<a id="advanced-operations"></a>
## 🛠️ Advanced Operations

### 🔄 Sync with Master (via Rebase)
To update your branch with a specific commit hash from the master branch:
```bash
git fetch origin master            # Fetch latest changes
git checkout <your-branch>         # Switch to your branch
git rebase <commit-hash>           # Rebase on specific commit
# Resolve conflicts if they occur
git rebase --continue              # Continue after conflict resolution
git push --force-with-lease        # Safely force push to remote
```

### 🏷️ Rename a Branch
To rename a branch both locally and on the remote:
```bash
# 1. Rename locally
git branch -m <new-name>

# 2. Delete old branch on remote
git push origin --delete <old-name>

# 3. Push new branch and set upstream
git push origin <new-name>
git push --set-upstream origin <new-name>
```

### 🔀 Merging Feature into Master
```bash
git checkout master                # Switch to master
git pull origin master             # Get latest master
git merge <your-branch>            # Merge your branch
# Resolve conflicts manually if any, then:
git add .
git commit -m "Merge <your-branch> into master"
git push origin master             # Push to remote
```

---
_Generated for a smoother Git experience._
