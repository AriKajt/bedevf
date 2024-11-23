
# How to Pull a GitHub Repository on a New Computer

This guide will walk you through the steps to pull a GitHub repository on a brand new computer. Make sure you have Git installed on your computer before proceeding.

## Step 1: Install Git

1. **Windows**
   - Download Git from [git-scm.com](https://git-scm.com/downloads).
   - Run the installer and follow the installation instructions.
   
2. **Linux**
   - Open a terminal and run:
     ```bash
     sudo apt update
     sudo apt install git
     ```
     
## Step 2: Configure Git

1. Open your terminal or Git Bash.
2. Set your Git username and email:
   ```bash
   git config --global user.name "Your Name"
   git config --global user.email "your.email@example.com"
   ```

## Step 3: Generate SSH Key (Optional)

If you want to use SSH for authentication:

1. Generate a new SSH key:
   ```bash
   ssh-keygen -t ed25519 -C "your.email@example.com"
   ```
   - Press Enter to accept the default location.
   - Enter a secure passphrase when prompted.

2. Start the SSH agent:
   ```bash
   eval "$(ssh-agent -s)"
   ```

3. Add your SSH key to the SSH agent:
   ```bash
   ssh-add ~/.ssh/id_ed25519
   ```

4. Copy the SSH key to your clipboard:
   ```bash
   cat ~/.ssh/id_ed25519.pub
   ```

5. Go to your GitHub account settings:
   - Navigate to **Settings > SSH and GPG keys**.
   - Click **New SSH key**.
   - Paste your SSH key and save.

## Step 4: Clone the Repository

1. Go to the GitHub repository page you want to pull.
2. Click the green **Code** button.
3. Copy the repository URL (either HTTPS or SSH).

### Using HTTPS:
   ```bash
   git clone https://github.com/username/repository.git
   ```

### Using SSH:
   ```bash
   git clone git@github.com:username/repository.git
   ```

4. Navigate to the repository directory:
   ```bash
   cd repository
   ```

## Step 5: Pull Changes from the Remote Repository

If you want to make sure you have the latest updates:

```bash
git pull origin main
```

Replace `main` with `master` if your default branch is named "master."

## Additional Git Commands

- **Check Git Status**: View changes in the working directory.
  ```bash
  git status
  ```
- **Add Changes**: Stage changes for commit.
  ```bash
  git add .
  ```
- **Commit Changes**: Commit staged changes.
  ```bash
  git commit -m "Your commit message"
  ```
- **Push Changes**: Push local commits to GitHub.
  ```bash
  git push origin main
  ```

## Troubleshooting

- **Authentication Error**: If you encounter authentication errors using HTTPS, make sure you've set up a Personal Access Token (PAT) for GitHub.
- **Permission Denied (Publickey)**: If you encounter this error using SSH, double-check that your SSH key is added to GitHub.
