# Git & GitHub Cheatsheet

A comprehensive reference guide for Git version control and GitHub collaboration.

## Table of Contents
- [Essential CLI Commands](#essential-cli-commands)
- [Git Configuration & Setup](#git-configuration--setup)
- [Git Basics](#git-basics)
- [File Management](#file-management)
- [Branching & Merging](#branching--merging)
- [Working with Remote Repositories](#working-with-remote-repositories)
- [GitHub Workflow](#github-workflow)
- [Advanced Git Operations](#advanced-git-operations)
- [Tags & Releases](#tags--releases)
- [Advanced Inspection](#advanced-inspection)
- [Security & .gitignore](#security--gitignore)
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

## Git Configuration & Setup

Think of Git configuration like setting up your personal workspace - you need to tell Git who you are and how you prefer to work.

### First-Time Setup (Do this once)
```bash
git --version                     # Check if Git is installed
git config --global user.name "Your Full Name"
git config --global user.email "your.email@example.com"
git config --global init.defaultBranch main
git config --global pull.rebase false
```

### Viewing & Managing Configuration
```bash
git config --list                # View all current settings
git config --global --list       # View only global settings
git config user.name             # Check specific setting
git config --global --unset setting.name  # Remove setting
```

### Useful Configuration Settings
```bash
# Make Git output more colorful
git config --global color.ui auto

# Set default editor (replace 'code' with your preferred editor)
git config --global core.editor "code --wait"

# Configure line ending handling (Windows users)
git config --global core.autocrlf true

# Configure line ending handling (Mac/Linux users)
git config --global core.autocrlf input
```

## Git Basics

### Initial Setup & Repository Creation
```bash
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

## File Management

Git isn't just about tracking changes - it can also help you manage files like a smart file system.

```bash
touch filename.txt         # Create new empty file
git add filename.txt       # Start tracking the file

# Renaming/Moving files (Git will track the change)
git mv old_name.txt new_name.txt
git mv file.txt folder/file.txt

# Removing files
rm filename.txt            # Delete from filesystem only
git rm filename.txt        # Remove from Git and filesystem
git rm --cached filename.txt  # Remove from Git but keep locally

# Cleaning up untracked files
git clean -n               # Preview what will be deleted
git clean -f               # Delete untracked files
git clean -fd              # Delete untracked files and directories
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

## Tags & Releases

Tags are like bookmarks for important moments in your project - think of them as placing a "milestone marker" at significant versions.

```bash
# Lightweight tags (simple bookmarks)
git tag v1.0.0                    # Tag current commit
git tag v1.0.0 commit_hash        # Tag specific commit

# Annotated tags (recommended for releases)
git tag -a v1.0.0 -m "Release version 1.0.0"
git tag -a v1.0.0 commit_hash -m "Stable release"

# Managing tags
git tag                           # List all tags
git tag -l "v1.*"                 # List tags matching pattern
git show v1.0.0                   # Show tag details
git tag -d v1.0.0                 # Delete local tag

# Sharing tags
git push origin v1.0.0            # Push specific tag
git push origin --tags            # Push all tags
git push origin --delete tag_name # Delete remote tag
```

## Advanced Inspection

Sometimes you need to be a detective and investigate your code's history - these commands help you analyze what happened and when.

```bash
# Detailed commit information
git show commit_hash              # Show specific commit details
git show HEAD~2                   # Show commit 2 steps back
git show --stat                   # Show commit with file statistics

# Comparing changes
git diff                          # Compare working directory to staging
git diff --staged                 # Compare staging to last commit  
git diff HEAD~1 HEAD              # Compare two commits
git diff branch1..branch2         # Compare two branches

# History and blame
git log --graph --oneline --all   # Visual branch history
git log --author="Name"           # Commits by specific author
git log --since="2 weeks ago"     # Commits in time period
git log --grep="fix"              # Search commit messages
git blame filename                # See who changed each line
git log -p filename               # See changes to specific file

# Finding bugs with binary search
git bisect start                  # Start bisect session
git bisect bad                    # Mark current commit as bad
git bisect good v1.0.0           # Mark known good commit
# Git will check out commits to test, mark each as good/bad
git bisect reset                  # End bisect session
```

## Security & .gitignore

Think of .gitignore as a bouncer at a club - it decides what gets in (tracked) and what stays out of your repository.

### Creating .gitignore
```bash
touch .gitignore              # Create .gitignore file
```

### Common .gitignore Patterns
```gitignore
# Compiled code
*.exe
*.dll
*.so
*.class

# Logs and databases
*.log
*.sqlite
*.db

# Environment and config files (NEVER commit these!)
.env
.env.local
config.ini
secrets.json

# Dependencies
node_modules/
__pycache__/
*.egg-info/
.venv/

# IDE and editor files
.vscode/
.idea/
*.swp
*.swo
*~

# Operating system files
.DS_Store
Thumbs.db
desktop.ini

# Build and dist directories  
build/
dist/
target/
*.tmp
*.temp

# Academic project specific
submission.zip
*.backup
```

### Managing .gitignore
```bash
git check-ignore filename        # Check if file is ignored
git add -f ignored_file          # Force add ignored file
git rm --cached file             # Stop tracking file (add to .gitignore after)
```

### Emergency: Removing Sensitive Files
```bash
# If you accidentally committed sensitive data
git rm --cached sensitive_file
echo "sensitive_file" >> .gitignore
git add .gitignore
git commit -m "Remove sensitive file and add to gitignore"

# For files in history, use git filter-branch or BFG Repo-Cleaner
# (Advanced - research thoroughly before using)
```

## Advanced Git Operations

### Commit Management
```bash
# Interactive rebase (rewrite commit history)
git rebase -i HEAD~3       # Interactive rebase for last 3 commits
# In editor: pick, squash, edit, reword, drop, or reorder commits

# Standard rebase (move branch to new base)
git rebase main            # Rebase current branch onto main
git rebase --continue      # Continue after resolving conflicts
git rebase --abort         # Cancel rebase and return to original state

# Squash commits (combine multiple commits into one)
git rebase -i HEAD~3       # Interactive rebase for last 3 commits
# In editor: change 'pick' to 'squash' for commits to combine

# Amend last commit
git commit --amend -m "Updated message"
git commit --amend --no-edit    # Add changes to last commit, keep message

# Cherry-pick (apply specific commit from another branch)
git cherry-pick commit_hash
git cherry-pick --no-commit commit_hash  # Cherry-pick without auto-commit

# Rebase vs Merge (Important distinction!)
# Rebase: Creates linear history, rewrites commits (cleaner but changes history)
# Merge: Preserves original history, creates merge commit (messier but safer)
```

## Advanced Git Operations

### Stashing (Enhanced)
```bash
git stash                     # Stash current changes
git stash save "work in progress"  # Stash with descriptive message
git stash list                # View all stashes
git stash show stash@{0}      # Show changes in specific stash
git stash apply stash@{1}     # Apply specific stash (keep in stash)
git stash pop stash@{1}       # Apply and remove specific stash
git stash drop stash@{1}      # Delete specific stash
git stash clear               # Delete all stashes
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
git diff --stat                    # See summary of changes
```

**Accidentally committed sensitive files:**
```bash
git rm --cached sensitive_file     # Remove from Git, keep locally
echo "sensitive_file" >> .gitignore  # Add to gitignore
git add .gitignore
git commit -m "Remove sensitive file from tracking"
```

**Accidentally deleted important files:**
```bash
git checkout HEAD -- filename     # Restore file from last commit
git checkout commit_hash -- filename  # Restore from specific commit
```

**Want to undo a merge:**
```bash
git reset --hard HEAD~1           # If merge was last commit
git revert -m 1 commit_hash       # Revert a merge commit safely
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
   - Good: "Fix login validation for empty email fields"
   - Bad: "Fixed bug" or "Updated code"
3. **Commit often** - small, logical chunks are better than large commits
4. **Pull before pushing** - avoid conflicts by staying up to date
5. **Use .gitignore properly** - never commit secrets, logs, or generated files
6. **One feature per branch** - keeps pull requests focused and manageable
7. **Tag important releases** - makes it easy to find and deploy specific versions
8. **Review your changes** - use `git diff --staged` before committing
9. **Keep commits atomic** - each commit should represent one logical change
10. **Use descriptive branch names** - `feature/user-authentication` not `my-branch`

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

## 📚 Learning Resources

### 🎮 Interactive Courses (Highly Recommended)

**[Boot.dev Git Courses](https://www.boot.dev/courses/learn-git)** ⭐ **Top Pick for CS Students**
- [Learn Git (Full Course)](https://www.boot.dev/courses/learn-git) - Covers fundamentals plus plumbing commands
- [Learn Git 2 (Advanced)](https://www.boot.dev/courses/learn-git-2) - Team collaboration, conflicts, and advanced workflows
- Interactive, hands-on learning with real coding challenges
- Perfect progression from beginner to professional developer
- Gamified learning experience that makes Git concepts stick

**Other Interactive Options:**
- [Learn Git Branching](https://learngitbranching.js.org/) - Visual, interactive Git tutorial
- [Git Immersion](https://gitimmersion.com/) - Guided tour through Git fundamentals
- [Katacoda Git Scenarios](https://www.katacoda.com/courses/git) - Browser-based Git practice

### 📖 Comprehensive Guides

**Beginner-Friendly:**
- [Git Handbook](https://guides.github.com/introduction/git-handbook/) - GitHub's official starter guide
- [Atlassian Git Tutorials](https://www.atlassian.com/git/tutorials) - Well-illustrated explanations
- [Git Tutorial for Beginners](https://www.freecodecamp.org/news/git-and-github-for-beginners/) - FreeCodeCamp guide

**Advanced References:**
- [Pro Git Book](https://git-scm.com/book) - The definitive free Git reference
- [Git Magic](http://www-cs-students.stanford.edu/~blynn/gitmagic/) - Stanford's advanced techniques guide
- [Git Internals](https://github.com/pluralsight/git-internals-pdf) - Understanding how Git works under the hood

### 🎥 Video Learning

- [Git & GitHub Crash Course](https://www.youtube.com/watch?v=RGOj5yH7evk) - Brad Traversy (1 hour)
- [Git Tutorial for Absolute Beginners](https://www.youtube.com/watch?v=CvUiKWv2-C0) - Tech with Tim
- [Advanced Git Tutorial](https://www.youtube.com/watch?v=Uszj_k0DGsg) - The Net Ninja series

### 🛠 Visual Git Tools (Great for Understanding)

- [GitKraken](https://www.gitkraken.com/) - Professional Git GUI with visual commit graphs
- [Sourcetree](https://www.sourcetreeapp.com/) - Free Git client by Atlassian
- [GitHub Desktop](https://desktop.github.com/) - Simple, user-friendly interface
- [GitLens](https://gitlens.amod.io/) - VS Code extension for Git visualization

### 📄 Quick References

- [GitHub Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf) - Official PDF cheat sheet
- [Atlassian Git Cheatsheet](https://www.atlassian.com/git/tutorials/atlassian-git-cheatsheet) - Command reference
- [Git Command Explorer](https://gitexplorer.com/) - Find commands by what you want to do

### 🎯 Practice Environments

- [GitHub](https://github.com/) - Create free repositories to practice
- [GitLab](https://gitlab.com/) - Alternative platform with built-in CI/CD
- [Bitbucket](https://bitbucket.org/) - Atlassian's Git platform
- [Codewars Git Kata](https://www.codewars.com/kata/search/git) - Git-specific coding challenges

### 📱 Mobile Learning

- [GitHub Mobile](https://github.com/mobile/) - Review code and manage repositories on mobile
- [Git Pocket Reference](https://www.oreilly.com/library/view/git-pocket-reference/9781449327507/) - O'Reilly pocket guide

### 🏫 Academic Resources

- [MIT's Version Control with Git](https://missing.csail.mit.edu/2020/version-control/) - Part of "Missing Semester" course
- [Stanford CS107 Git Guide](https://web.stanford.edu/class/cs107/guide/git.html) - Academic perspective
- [Berkeley CS61B Git Guide](https://sp21.datastructur.es/materials/guides/git-wtfs.html) - Common Git problems for students

**💡 Recommended Learning Path:**
1. Start with **Boot.dev's Git course** for solid fundamentals
2. Practice with **Learn Git Branching** for visual understanding  
3. Use this cheatsheet as your daily reference
4. Try **Boot.dev's advanced Git course** when ready for team workflows
5. Keep **Pro Git Book** as your comprehensive reference

For more detailed information, visit the [official Git documentation](https://git-scm.com/doc).
