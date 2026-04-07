# Initializing Git to a project  
- git init
- git add  .
- git commit -m ""
- git branch -M main
- git remote add origin https://<your_github_repo_url>/<project_name>.git
- git push -U origin main

# Adding Changes to a specific branch
- git status
- git add .
- git commit -m ""
- git push origin <branch_name>

# Getting the latest state of a Brach
- git pull origin <branch_name>

# Creating a new Branch and Entering to it 
- git branch <branch_name>
- git checkout <branch_name>

# Deleting a branch
- git branch -D <branch_name>

# Merging a Branch 
- Go To the specific branch u wanted to be merge with
- git branch
- main* // this shows that you are in the main branch
- bugFix
- git merge bugFix // u js merged bugFix into the main.

# Git Revert commonly used for Shared Env.
- It DOES NOT erase History in commit 
- Good for undo a member commit 
- git revert <commit_hash>
- git commit -m "Revert `LoginFeature`"
- git push

# Git Reset (Soft & Hard)
## Soft Reset - removes History in commit but all the changes are staged and ready for modification or deletion.
- git reset --soft <commit_hash>

## Hard Reset - removes commit history above it along with all of the code 
- git reset --hard <commit_hash>
