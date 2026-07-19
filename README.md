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
- [🏷️ Tagging](#tagging)
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
| `git config --global core.editor <editor>` | Set the default text editor used by Git (e.g., `nano`, `code`). |
| `git config --global alias.<alias-name> <command>` | Set a custom shortcut/alias for a command (e.g., `git config --global alias.co checkout`). |

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
| `git config --global credential.helper cache` | Cache your credentials in memory for a short time (e.g., 15 mins). |

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
| `git status -s` | Show status in a short, concise format. |
| `git add <file>` | Add a specific file to the staging area. |
| `git add .` | Add all new, modified, and deleted files to the staging area. |
| `git commit -m "[message]"` | Commit staged changes with a descriptive message. |
| `git commit -am "[message]"` | Stage all tracked modified files and commit in one step. |
| `git restore <file>` | Discard unstaged changes in the working directory (alternative to `git checkout -- <file>`). |
| `git restore --staged <file>` | Unstage a file but keep its local modifications (alternative to `git reset HEAD <file>`). |
| `git push origin <branch>` | Push local branch commits to the remote repository. |
| `git pull` | Fetch from and integrate with another repository or a local branch (fetch + merge). |
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
| `git switch <branch-name>` | Switch to a different branch (modern alternative to `checkout`). |
| `git checkout -b <branch-name>` | Create a new branch and switch to it immediately. |
| `git switch -c <branch-name>` | Create a new branch and switch to it immediately (modern alternative to `checkout -b`). |
| `git checkout -b <name> origin/<name>` | Clone a remote branch and switch to it. |
| `git branch -d <branch-name>` | Delete a local branch (must be merged first). |
| `git branch -D <branch-name>` | Force delete a local branch. |
| `git merge <branch-name>` | Merge the specified branch into the current one. |
| `git merge --abort` | Abort the current merge conflict and restore the pre-merge state. |
| `git merge --no-ff <branch-name>` | Merge the branch but force a merge commit even if fast-forward is possible. |
| `git checkout -` | Switch to the branch last checked out. |

---

<a id="stashing-cleaning"></a>
## 📦 Stashing & Cleaning

| Command | Description |
| :--- | :--- |
| `git stash` | Temporarily store all modified tracked files. |
| `git stash push -m "[message]"` | Save stashed changes with a custom description. |
| `git stash list` | List all stashed changes. |
| `git stash pop` | Restore the most recently stashed files and remove them from stash. |
| `git stash apply` | Restore stashed files without removing them from stash. |
| `git stash drop stash@{n}` | Delete a specific stash from the stash list. |
| `git stash clear` | Remove all stashed entries. |
| `git clean -n` | Dry run: Show which untracked files will be removed. |
| `git clean -fd` | Force clean: Remove all untracked files and directories. |
| `git rm -r <file>` | Remove a file (or folder) and stage the deletion. |
| `git rm -r --cached <file>` | Remove a file from version control but keep it locally. |

---

<a id="inspection-comparison"></a>
## 🔍 Inspection & Comparison

| Command | Description |
| :--- | :--- |
| `git log` | Show the commit history for the current branch. |
| `git log --oneline` | Show commit history in a condensed, one-line format. |
| `git log --graph --oneline --all --decorate` | Display a text-based graphical tree of all commits, tags, and branches. |
| `git log --summary` | View changes with detailed statistics (files changed, etc.). |
| `git log -p <file>` | Show commit history with detailed diffs for a specific file. |
| `git show <commit-hash>` | Show the metadata and content differences of a specific commit. |
| `git show <commit-hash>:<file>` | View the content of a file at a specific commit. |
| `git diff <source> <target>` | Preview changes between two branches before merging. |
| `git diff --staged` | Show differences between the staging area and the last commit. |
| `git blame <file>` | Display the author and commit hash for each line of a file. |
| `git reflog` | Show a local log of all reference changes (commits, checkouts, resets). |

---

<a id="undo-recover-panic-section"></a>
## 🚨 Undo & Recover (The "Panic" Section)

| Command | Description |
| :--- | :--- |
| `git reset <file>` | Unstage a file, keeping the changes in the working directory. |
| `git restore --staged <file>` | Unstage a file, keeping changes in the working directory (modern alternative to `git reset`). |
| `git checkout -- <file>` | Discard changes to a specific file (restore from last commit). |
| `git restore <file>` | Discard changes to a specific file (restore from last commit; modern alternative to `git checkout --`). |
| `git checkout <commit-hash> -- <file>` | Restore a specific file from a specific past commit. |
| `git restore --source=<commit-hash> <file>` | Restore a specific file from a specific past commit (modern alternative to `git checkout ... --`). |
| `git commit --amend` | Replace the last commit with a new one (useful for fixing message/files). |
| `git revert <commit-hash>` | Create a new commit that undoes the changes of a past commit (safe for shared branches). |
| `git reset --soft <commit-hash>` | Reset branch history to a commit, keeping changes staged in the staging area. |
| `git reset <commit-hash>` | Reset branch history to a commit, keeping changes unstaged in the working directory. |
| `git reset --hard <commit-hash>` | **WARNING:** Reset everything to a specific commit. All local changes will be lost. |
| `git push -f origin <branch>` | **WARNING:** Force push changes to remote (use with caution). |

### 🔄 Reset Branch to a Specific Commit
To reset your local branch and remote repository back to a specific commit:
```bash
git reset --hard <commit-hash>      # WARNING: Reset everything to a specific commit. All local changes will be lost.
git push -f origin <branch-name>    # WARNING: Force push changes to remote (use with caution).
```

---

<a id="tagging"></a>
## 🏷️ Tagging

| Command | Description |
| :--- | :--- |
| `git tag` | List all tags in the repository. |
| `git tag -a <tag-name> -m "[message]"` | Create an annotated tag with a descriptive message. |
| `git tag <tag-name>` | Create a lightweight tag at the current commit. |
| `git tag -d <tag-name>` | Delete a tag locally. |
| `git push origin <tag-name>` | Push a specific tag to the remote repository. |
| `git push origin --tags` | Push all local tags to the remote repository. |
| `git push origin --delete <tag-name>` | Delete a tag from the remote repository. |

---

<a id="remote-repository-management"></a>
## 🚀 Remote Repository Management

| Command | Description |
| :--- | :--- |
| `git remote set-url origin <url>` | Change the remote repository URL (e.g., switch to SSH). |
| `git push -u origin <branch>` | Push and set the remote as the default upstream. |
| `git push origin --delete <branch>` | Delete a branch from the remote repository. |
| `git remote prune origin` | Remove local references to deleted remote branches. |
| `git fetch` | Download objects and refs from another repository without merging. |
| `git remote rename <old> <new>` | Rename a remote server connection. |
| `git remote remove <name>` | Remove a remote server connection. |
| `git push origin <local-branch>:<remote-branch>` | Push to a remote branch with a different name. |

---

<a id="advanced-operations"></a>
## 🛠️ Advanced Operations

### 🍒 Cherry-picking
Apply the changes introduced by an existing commit to your current branch:
```bash
git cherry-pick <commit-hash>      # Apply specific commit to current branch
```

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

### ⚙️ Interactive Rebase
Edit, squash, reorder, or delete commits in your branch history:
```bash
git rebase -i HEAD~<number>        # Interactively rebase the last <number> of commits
# In the interactive text editor, change 'pick' to 'squash' (or 's'), 'reword' (or 'r'), etc.
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

### 📂 Git Submodules
Manage nested/external repositories inside your repository:
```bash
git submodule add <url>                     # Add external repo as a submodule
git submodule init                          # Initialize your local configuration file
git submodule update --init --recursive     # Initialize and update submodules recursively (e.g. after clone)
```

### 🔍 Git Bisect (Bug Hunting)
Find the specific commit that introduced a bug using binary search:
```bash
git bisect start                   # Start the bisecting process
git bisect bad                     # Mark current commit as bad/broken
git bisect good <commit-hash>      # Mark a known working commit as good
# Git will checkout a commit in the middle. Test the code:
git bisect good                    # If code works
# or
git bisect bad                     # If code is broken
# Repeat until Git identifies the exact bad commit. To exit:
git bisect reset                   # Return to original branch/commit
```

---
_Generated for a smoother Git experience._
