
#!/bin/bash

# Function to display script usage
display_usage() {
  echo "Script usage: $0 <GITHUB_USERNAME> <GITHUB_TOKEN>"
  echo "Arguments:"
  echo "  <GITHUB_USERNAME>   Your GitHub username."
  echo "  <GITHUB_TOKEN>      Your GitHub Personal Access Token (PAT) for authentication."
}

# Function to add, commit, and push changes to an existing Git repository
push_changes() {
  # Add files to the repository
  git add .

  # Commit the changes
  git commit -m "$REPO_NAME is public now"

  # Push to GitHub
  git push -u origin master

  echo "Changes pushed to the GitHub repository successfully!"
}

# Parse command-line arguments
if [[ $# -ne 2 ]]; then
  display_usage
  exit 1
fi

GITHUB_USERNAME=$1
GITHUB_TOKEN=$2
REPO_NAME=$(basename "$(pwd)")

# Check if the directory already exists as a Git repository
if [ -d .git ]; then
  echo "Git repository already exists. Adding, committing, and pushing changes..."
  push_changes
else
  echo "Git repository not found. Creating a new GitHub repository..."

  # Authenticate with GitHub and create the repository
  curl -u "$GITHUB_USERNAME:$GITHUB_TOKEN" https://api.github.com/user/repos -d "{\"name\":\"$REPO_NAME\"}"

  # Initialize a local Git repository
  git init

  # Add files to the repository
  git add .

  # Commit the changes
  git commit -m "$REPO_NAME is public now"

  # Add the remote repository
  git remote add origin "https://github.com/$GITHUB_USERNAME/$REPO_NAME.git"

  # Push to GitHub
  git push -u origin master

  echo "GitHub repository created and initial commit pushed successfully!"
fi
