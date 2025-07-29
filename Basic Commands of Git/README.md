# Essential Git Commands

A detailed reference guide to the most critical Git commands that every developer should master for efficient version control and collaboration.

## 📁 Repository Setup
```bash
git init                    # Initialize a new Git repository
git clone <url>            # Clone an existing repository
```

## Basic Workflow
```bash
git status                 # Check repository status
git add <file>            # Add file(s) to staging area
git add .                 # Add all changes to staging
git commit -m "message"   # Commit staged changes
git commit -am "message"  # Add and commit in one command
```

## Branching
```bash
git branch                 # List all branches
git branch <name>         # Create a new branch
git checkout <branch>     # Switch to a branch
git checkout -b <name>    # Create and switch to new branch
git merge <branch>        # Merge branch into current branch
git branch -d <name>      # Delete a branch
```

## Remote Operations
```bash
git remote -v             # View remote repositories
git remote add origin <url> # Add remote repository
git push                  # Push changes to remote
git push -u origin <branch> # Push and set upstream
git pull                  # Fetch and merge from remote
git fetch                 # Fetch changes from remote
```

## History and Logs
```bash
git log                   # View commit history
git log --oneline         # View compact commit history
git log --graph           # View history with branch graph
git diff                  # Show unstaged changes
git diff --staged         # Show staged changes
git show <commit>         # Show specific commit details
```

## Undo Operations
```bash
git reset <file>          # Unstage a file
git reset --hard          # Discard all changes
git checkout -- <file>    # Discard changes in working directory
git revert <commit>       # Create new commit that undoes changes
```

## Tags
```bash
git tag                   # List tags
git tag <name>            # Create lightweight tag
git tag -a <name> -m "msg" # Create annotated tag
git push --tags           # Push tags to remote
```

### Useful Tips
- Use git config --global user.name "Your Name" to set your identity
- Use git config --global user.email "email@example.com" for email
- git stash temporarily saves changes
- git blame <file> shows who modified each line