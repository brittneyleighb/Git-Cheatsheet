# Git & GitHub Cheatsheet

A comprehensive reference guide for Git version control and GitHub collaboration.

## Table of Contents
- [Essential CLI Commands](#essential-cli-commands)
- [Git Basics](#git-basics)
- [Branching & Merging](#branching--merging)
- [Working with Remote Repositories](#working-with-remote-repositories)
- [GitHub Workflow](#github-workflow)
- [Advanced Git Operations](#advanced-git-operations)
- [Troubleshooting](#troubleshooting)

## Essential CLI Commands

### File & Directory Operations
```bash
ls                          # List files and folders
mkdir folder_name          # Create new folder
cd folder_name             # Navigate into folder
rm -rf directory_name      # Delete directory and contents (use with caution!)
touch filename.txt         # Create new file
```

### Text Editor (Vim)
```bash
vim filename               # Open file in Vim
# Press 'i' to enter insert mode
# Press 'Esc' then ':x' to save and exit
# Press 'Esc' then ':q!' to quit without saving
```

## Git Basics

### Initial Setup & Repository Creation
```bash
git --version              # Check if Git is installed
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
git init                   # Initialize new Git repository
```

### The Git Workflow (Think of it as a Photo Development Process)
```bash
# 1. Working Directory (Taking photos)
git status                 # Check what's changed (see which photos you've taken)

# 2. Staging Area (Selecting photos for album)
git add filename           # Stage specific file
git add .                  # Stage all changes
git restore --staged file # Remove file from staging

# 3. Repository (Publishing the album)
git commit -m "message"    # Commit staged changes
git log                    # View commit history
git log --oneline         # Compact commit history
```

### Undoing Changes
```bash
git restore filename       # Discard changes in working directory
git reset HEAD~1          # Undo last commit (keep changes)
git reset --hard HEAD~1   # Undo last commit (discard changes)
git stash                 # Temporarily save changes
git stash pop             # Retrieve stashed changes
git stash clear           # Delete all stashed changes
```

## Branching & Merging

Think of branches like parallel universes where you can experiment without affecting the main timeline.

```bash
git branch                 # List all branches
git branch branch_name     # Create new branch
git checkout branch_name   # Switch to branch
git checkout -b new_branch # Create and switch to new branch
git merge branch_name      # Merge branch into current branch
git branch -d branch_name  # Delete branch (safe)
git branch -D branch_name  # Force delete branch
```

## Working with Remote Repositories

### Connecting Local to Remote (Like linking your phone to the cloud)
```bash
git remote add origin https://github.com/username/repo.git
git remote -v              # View remote URLs
git push -u origin main    # Push and set upstream
git push origin branch_name # Push specific branch
```

### Fetching & Pulling Changes
```bash
git fetch origin           # Download changes (don't merge)
git pull origin main       # Download and merge changes
git clone repo_url         # Copy remote repository locally
```

## GitHub Workflow

### Forking & Contributing (Like making your own copy of a recipe to modify)

1. **Fork the repository** on GitHub (creates your copy)
2. **Clone your fork** locally:
   ```bash
   git clone your_fork_url
   ```

3. **Add upstream remote** (link to original repository):
   ```bash
   git remote add upstream original_repo_url
   ```

4. **Create feature branch**:
   ```bash
   git checkout -b feature/new-feature
   ```

5. **Make changes, stage, and commit**:
   ```bash
   git add .
   git commit -m "Add new feature"
   ```

6. **Push to your fork**:
   ```bash
   git push origin feature/new-feature
   ```

7. **Create Pull Request** on GitHub

### Keeping Fork Updated
```bash
# Method 1: Fetch and reset
git fetch --all --prune
git checkout main
git reset --hard upstream/main
git push origin main

# Method 2: Pull and push
git checkout main
git pull upstream main
git push origin main
```

## Advanced Git Operations

### Commit Management
```bash
# Squash commits (combine multiple commits into one)
git rebase -i HEAD~3       # Interactive rebase for last 3 commits
# In editor: change 'pick' to 'squash' for commits to combine

# Amend last commit
git commit --amend -m "Updated message"

# Cherry-pick (apply specific commit from another branch)
git cherry-pick commit_hash
```

### Conflict Resolution
When Git can't automatically merge changes (like two editors changing the same sentence):

1. Git will mark conflicts in files:
   ```
   <<<<<<< HEAD
   Your changes
   =======
   Their changes
   >>>>>>> branch-name
   ```

2. Edit files to resolve conflicts
3. Stage resolved files: `git add filename`
4. Complete the merge: `git commit`

## Troubleshooting

### Common Issues & Solutions

**Accidentally committed to main branch:**
```bash
git checkout -b feature/new-branch  # Create new branch
git checkout main                   # Switch to main
git reset --hard HEAD~1            # Remove commit from main
```

**Need to force push after rebase:**
```bash
git push origin branch_name -f     # Use with caution!
```

**Want to see changes before committing:**
```bash
git diff                           # See unstaged changes
git diff --staged                  # See staged changes
```

**Forgot what you were working on:**
```bash
git status                         # Check current state
git log --oneline -5              # See recent commits
git stash list                    # See stashed changes
```

## Best Practices

1. **Never commit directly to main/master** - always use feature branches
2. **Write meaningful commit messages** - describe what and why, not how
3. **Commit often** - small, logical chunks are better than large commits
4. **Pull before pushing** - avoid conflicts by staying up to date
5. **Use .gitignore** - don't commit generated files, logs, or secrets
6. **One feature per branch** - keeps pull requests focused and manageable

## Useful Aliases

Add these to your `~/.gitconfig` file:
```ini
[alias]
    st = status
    co = checkout
    br = branch
    ci = commit
    unstage = reset HEAD --
    last = log -1 HEAD
    visual = !gitk
```

---

**Remember:** Git is like a time machine for your code. Every commit is a snapshot you can return to, and branches let you explore different possibilities without losing your work!

For more detailed information, visit the [official Git documentation](https://git-scm.com/doc).
