# 👤 GitHub Accounts Handling Using Git

Complete guide to managing GitHub accounts, authentication, and credentials with Git.

## 🔐 Authentication Methods

### 1. HTTPS with Personal Access Token (Recommended)
```bash
git clone https://github.com/username/repository_name.git
# When prompted, enter username and Personal Access Token
```

### 2. SSH Keys (Most Secure)
```bash
# Generate SSH key
ssh-keygen -t ed25519 -C "your_email@example.com"

# Start SSH agent
eval "$(ssh-agent -s)"

# Add SSH key
ssh-add ~/.ssh/id_ed25519

# Test connection
ssh -T git@github.com
```

### 3. GitHub CLI Authentication
```bash
# Install GitHub CLI
gh auth login
```

## Multiple GitHub Accounts

### Setting Up Multiple Accounts
```bash
# Configure different users for different repositories
git config user.name "work-username"
git config user.email "work@example.com"

# Global configuration (default)
git config --global user.name "personal-username"
git config --global user.email "personal@example.com"
```

### Repository-Specific Configuration
```bash
# In specific repository
git config user.name "specific-username"
git config user.email "specific@example.com"

# Verify configuration
git config --list
```

## Credential Management

### Configure Credential Helper
```bash
# Cache credentials temporarily (default 15 minutes)
git config --global credential.helper cache

# Cache with custom timeout (1 hour)
git config --global credential.helper 'cache --timeout=3600'

# Store credentials permanently (less secure)
git config --global credential.helper store

# Use OS-specific credential manager
git config --global credential.helper manager-core  # Windows
```

### View Current Credentials
```bash
git config --global credential.helper
git credential-manager-core list  # Windows
```

### Manual Credential Update
**For Windows:**
- Go to Windows Credentials
- Find GitHub credentials and remove them
- Next git operation will prompt for new credentials

**For Mac:**
```bash
# Remove keychain entry
git credential-osxkeychain erase
# Host: github.com
# Protocol: https
# Press Enter twice
```

**For Linux:**
```bash
# Clear cached credentials
git credential-cache exit
```

## Clearing Stored Credentials

### Remove All Cached Credentials
```bash
# Clear credential cache
git config --global --unset credential.helper
git credential-cache exit

# Remove specific credential helper
git config --global --unset-all credential.helper
```

### Remove Single Credential
```bash
# For credential store
git config --global --unset credential.helper store

# For credential cache
git credential-cache exit
```

## Troubleshooting Authentication

### Check Current Authentication
```bash
# Test HTTPS authentication
git ls-remote https://github.com/username/repository.git

# Test SSH authentication
ssh -T git@github.com
```

### Fix Authentication Issues
```bash
# Update remote URL to use HTTPS with token
git remote set-url origin https://username:token@github.com/username/repository.git

# Update remote URL to use SSH
git remote set-url origin git@github.com:username/repository.git

# Verify remote URL
git remote -v
```

## Switching Between Accounts

### Method 1: Repository-Specific Configuration
```bash
# In repository directory
git config user.name "new-username"
git config user.email "new@example.com"

# Verify changes
git config user.name
git config user.email
```

### Method 2: Using Different SSH Keys
```bash
# Create/configure SSH config file
nano ~/.ssh/config

# Add configuration:
# Host github-work
#   HostName github.com
#   User git
#   IdentityFile ~/.ssh/id_rsa_work
#
# Host github-personal
#   HostName github.com
#   User git
#   IdentityFile ~/.ssh/id_rsa_personal

# Clone using specific host
git clone git@github-work:company/repository.git
```

## Personal Access Tokens

### Creating PAT (Classic)
- Go to GitHub Settings → Developer settings → Personal access tokens
- Click "Generate new token"
- Select required scopes
- Generate and copy token

### Using PAT with Git
```bash
# Clone with token
git clone https://username:token@github.com/username/repository.git

# Update remote URL with token
git remote set-url origin https://username:token@github.com/username/repository.git
```

### Revoking PAT
```bash
# Update to remove token from URL
git remote set-url origin https://github.com/username/repository.git
```

## Advanced Account Management

### Configure Different Remotes for Different Accounts
```bash
# Add multiple remotes
git remote add origin-personal https://github.com/personal/repo.git
git remote add origin-work https://github.com/work/repo.git

# Push to specific remote
git push origin-personal main
git push origin-work main
```

### Using Environment Variables for Tokens
```bash
# Set environment variable
export GITHUB_TOKEN=your_token_here

# Use in scripts
git clone https://username:${GITHUB_TOKEN}@github.com/username/repo.git
```

## Common Commands for Account Handling

### View Current Configuration
```bash
git config --list --show-origin
git config user.name
git config user.email
git remote -v
```

### Update User Information
```bash
# Global (all repositories)
git config --global user.name "New Name"
git config --global user.email "new@example.com"

# Local (current repository only)
git config user.name "Repo Specific Name"
git config user.email "repo@example.com"
```

### Reset Authentication
```bash
# Remove all stored credentials
git config --global --unset credential.helper
git credential-cache exit

# Reconfigure credential helper
git config --global credential.helper cache
```