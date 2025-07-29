# Uploading Files to GitHub Using Git

Complete step-by-step guide to upload files to GitHub using Git commands.

## Prerequisites

1. **Install Git** on your system
2. **Create a GitHub account**
3. **Configure Git with your identity**:
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

# Method 1: Upload to Existing Repository 

### Step 1: Clone the Repository
```bash
git clone https://github.com/username/repository-name.git
cd repository-name
```

### Step 2: Add Your Files
```bash
# Copy your files to the repository directory
cp /path/to/your/files/* .

# Or create new files directly
echo "Hello World" > new-file.txt
```

### Step 3: Stage and Commit Files
```bash
git add .                          # Add all files
git add filename.txt               # Add specific file
git add *.jpg                      # Add all JPEG files

git status                         # Check what will be committed
git commit -m "Add new files"
```

### Step 4: Push to GitHub
```bash
git push origin main               # Push to main branch
git push origin master             # Push to master branch (older repos)
```

# Method 2: Create New Repository and Upload

### Step 1: Create Repository on GitHub
- Go to GitHub
- Click "New repository"
- Enter repository name
- Choose visibility (Public/Private)
- Don't initialize with README

### Step 2: Initialize Local Repository
```bash
# Create project directory
mkdir my-project
cd my-project

# Initialize Git repository
git init
```

### Step 3: Add Files to Repository
```bash
# Add your project files
echo "# My Project" > README.md
echo "node_modules/" > .gitignore
# Add other project files...

# Stage all files
git add .

# Commit files
git commit -m "Initial commit"
```

### Step 4: Connect to GitHub and Push
```bash
# Add remote origin (replace with your repo URL)
git remote add origin https://github.com/username/repository-name.git

# Push to GitHub
git branch -M main                 # Rename branch to main (optional)
git pull origin main               # Fetch and merge remote changes
git push -u origin main            # First push with upstream tracking
git push -u origin main --force-with-lease # if throw error then used safer force push
```

## Working with Different File Types

### Upload Code Files
```bash
git add *.js *.css *.html          # Add specific file types
git add src/                       # Add entire directory
git add .                          # Add all files
git commit -m "Add source code"
git push
```

### Upload Images
```bash
git add *.png *.jpg *.gif
git commit -m "Add images"
git push
```

### Upload Documents
```bash
git add *.pdf *.docx *.md
git commit -m "Add documentation"
git push
```

### Managing Large Files
```bash
# Install Git LFS (Large File Storage)
git lfs install

# Track specific file types
git lfs track "*.psd"
git lfs track "*.zip"

# Add and commit normally
git add .gitattributes
git add large-file.psd
git commit -m "Add large file with LFS"
git push
```

## Advanced Upload Scenarios

### Upload to Specific Branch
```bash
git checkout -b new-feature        # Create and switch to new branch
# Add your files...
git add .
git commit -m "Add feature files"
git push origin new-feature        # Push to specific branch
```

### Upload with Tags
```bash
git add .
git commit -m "Release version 1.0"
git tag -a v1.0 -m "Version 1.0"
git push origin main
git push origin --tags             # Push tags to GitHub
```