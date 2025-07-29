# 📁 Git File Handling

Complete guide to managing files with Git commands and operations.

## 📝 File Tracking and Staging

### Adding Files
```bash
git add <file>             # Add specific file to staging area
git add .                  # Add all changes in current directory
git add *.txt              # Add all .txt files
git add docs/              # Add all files in docs directory
git add -A                 # Add all changes (new, modified, deleted)
```

### Removing Files
```bash
git rm <file>              # Remove file from both working directory and index
git rm --cached <file>     # Remove file from index only (stop tracking)
git rm -r <directory>      # Remove directory and all its contents
git rm *.log               # Remove all .log files
```

### Moving/Renaming Files
```bash
git mv <old> <new>         # Move or rename file
git mv file.txt newfile.txt # Rename file
git mv file.txt docs/      # Move file to directory
```

## Checking File Status

### Status Commands
```bash
git status                 # Show working tree status
git status -s              # Short format status
git status --porcelain     # Machine-readable status
```

### File Status Symbols
- ?? - Untracked files
- A - Added files
- M - Modified files
- D - Deleted files
- R - Renamed files

## File Comparison
```bash
git diff                   # Show unstaged changes
git diff --staged          # Show staged changes
git diff HEAD              # Show all changes (staged and unstaged)
git diff <file>            # Show changes in specific file
git diff <commit1> <commit2> # Compare two commits
git diff HEAD~1 HEAD       # Compare last two commits
```

### Ignoring Files
```bash
# Ignore specific files
*.log
*.tmp
config.ini

# Ignore directories
node_modules/
dist/
build/

# Ignore all files in directory except specific ones
logs/*
!important.log

# Ignore files with specific pattern
temp-[0-9]*.txt
```

### Global Git Ignore
```bash
git config --global core.excludesfile ~/.gitignore_global
```

## Recovering Files

### Restore Commands
```bash
git restore <file>         # Restore file from last commit
git restore --staged <file> # Unstage file
git checkout -- <file>     # Restore file (older syntax)
git checkout <commit> -- <file> # Restore file from specific commit
```

### Recovering Deleted Files
```bash
git checkout HEAD -- <file>    # Restore deleted file
git checkout <commit> -- <file> # Restore file from specific commit
```

## File Information

### Log for Specific Files
```bash
git log --follow <file>    # Track file history including renames
git log -p <file>          # Show commits with file changes
git blame <file>           # Show who modified each line
git blame -L 10,20 <file>  # Blame specific lines
```

### File Archives and Exports
```bash
git archive HEAD --format=zip --output=project.zip
git archive HEAD docs/ --format=zip --output=docs.zip
git archive --prefix=project/ HEAD | tar -xzf -
```

## Advanced File Operations

### Partial Staging
```bash
git add -p <file>          # Interactively stage parts of file
git add --patch            # Same as above
```

### Clean Working Directory
```bash
git clean -n               # Preview what would be removed
git clean -f               # Remove untracked files
git clean -fd              # Remove untracked files and directories
git clean -fx              # Remove untracked and ignored files
```

### Working with Files Across Branches
```bash
git checkout <branch> -- <file>    # Get file from another branch
git show <branch>:<file>           # Show file content from branch
git diff <branch1> <branch2> -- <file> # Compare file between branches
```

## Useful File Handling Tips

### Configuration 
```bash
git config core.autocrlf true      # Handle line endings (Windows)
git config core.autocrlf input     # Handle line endings (Mac/Linux)
git config core.ignorecase false   # Case-sensitive file names
```

### Performance
```bash
git gc                     # Optimize repository
git fsck                   # Check repository integrity
git count-objects -v       # Show repository size information
```

## Common File Handling Scenarios

### Scenario 1: Accidentally Added File
```bash
git reset <file>           # Unstage file
git rm --cached <file>     # Stop tracking file
```

### Scenario 2: Large File Added by Mistake
```bash
git filter-branch --force --index-filter \
'git rm --cached --ignore-unmatch <file>' \
--prune-empty --tag-name-filter cat -- --all
```

### Scenario 3: Case-Sensitive File Rename
```bash
git mv file.txt temp
git mv temp FILE.txt
```