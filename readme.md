# Comprehensive Git Command Reference

This guide provides an overview of essential Git commands, including tips for managing commits, tracking branches, and dealing with untracked files.

---

## 1. Initializing a Git Repository
```
git init
```
Transforms a folder into a trackable Git repository. Think of it as "turning on" Git for the folder.

---

## 2. Checking Repository Status
```
git status
```
Displays the state of your working directory and staging area. Shows untracked, modified, and staged files.

---

## 3. Creating and Staging Files
**Add a Single File to Staging Area:**
```
git add [file_name]
```

**Add All Files to Staging Area:**
```
git add .
```

**Unstage Files:**
```
git reset [file_name]
```
Removes a file from the staging area without deleting it.

---

## 4. Committing Changes
```
git commit -m "[message]"
```
Captures a snapshot of the staged changes.  
Example:  
```
git commit -m "Initial commit"
```

---

## 5. Viewing Commit History
```
git log
```
Shows a detailed list of commits in the repository history.

**View Specific Commit:**
```
git show [commit_hash]
```
Displays details of a specific commit.

---

## 6. Deleting Commits

**Delete Last Local Commit (Keep Changes):**
```
git reset --soft HEAD~1
```
Removes the last commit from history but keeps the changes in the staging area.

**Delete Last Local Commit (Discard Changes):**
```
git reset --hard HEAD~1
```
Completely deletes the last commit and discards all changes.

**Undo a Pushed Commit:**

1. Reset to a Previous Commit Locally:  
```
git reset --hard [commit_hash]
```

2. Force Push Changes to Remote:  
```
git push origin [branch_name] --force
```

---

## 7. Cloning a Repository
```
git clone [repository_url]
```
Creates a local copy of a remote repository.

---

## 8. Tracking and Managing Branches

**List All Branches:**
```
git branch
```

**Create a New Branch:**
```
git branch [branch_name]
```

**Switch to a Branch:**
```
git switch [branch_name]
```

**Create and Switch to a New Branch:**
```
git checkout -b [branch_name]
```

**Track a Remote Branch:**
```
git branch --set-upstream-to=origin/[branch_name] [local_branch]
```

**Delete a Local Branch:**
```
git branch -d [branch_name]
```

**Delete a Remote Branch:**
```
git push origin --delete [branch_name]
```

---

## 9. Merging Branches
```
git merge [branch_name]
```
Combines changes from the specified branch into the current branch.

---

## 10. Handling Untracked Files

**View Untracked Files:**
```
git status
```

**Ignore Files Permanently:**  
Add file patterns to `.gitignore`. Example:

```
# Ignore all .log files
*.log
```

Commit the `.gitignore` file:

```
git add .gitignore
git commit -m "Add .gitignore"
```

---

## 11. Pushing Changes
```
git push origin [branch_name]
```
Pushes changes to a remote repository.

---

## 12. Pulling Changes
```
git pull
```
Fetches and integrates changes from the remote repository into the current branch.

---

## 13. Updating Local Branch to Track Remote
```
git fetch
```
Updates references to the remote repository.

```
git checkout -b [branch_name] origin/[branch_name]
```
Creates and tracks a local branch to match the remote one.

---

## 14. Resolving Common Issues

### Accidentally Commit to the Wrong Branch:
1. Reset the Commit Locally:  
```
git reset HEAD~1
```

2. Switch to the Correct Branch:  
```
git switch [branch_name]
```

3. Apply the Changes:  
```
git add . && git commit -m "[message]"
```

### Revert a Commit (Without Deleting History):
```
git revert [commit_hash]
```
Creates a new commit to undo changes from the specified commit.

---

## 15. Checking Remote Repositories

**View Remote URLs:**
```
git remote -v
```

**Add a Remote Repository:**
```
git remote add origin [url]
```

---

## 16. Helpful Shortcuts and Tips

**View All Commits in a Branch:**
```
git log --oneline
```

**Discard Local Changes in a File:**
```
git checkout -- [file_name]
```

**View Changes Before Staging:**
```
git diff
```

**View Changes After Staging:**
```
git diff --cached
```

**Stash Changes Temporarily:**
```
git stash
```
Save uncommitted changes to a temporary area.

**Apply Stashed Changes:**
```
git stash pop
```

---

## 17. Configuring Git (Name & Email)

To configure your name and email for Git commits:
```
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

To verify your configuration:
```
git config --list
```

---

## 18. Standard Git Flow

Here's a typical Git workflow that includes initialization, adding a README, linking a remote repository, and pushing changes:

1. Initialize a new Git repository:
```
git init
```

2. Create a `README.md` file and add it to the repository:
```
echo "# My Project" > README.md
git add README.md
git commit -m "Add README"
```

3. Add a remote repository:
```
git remote add origin [remote_repo_url]
```

4. Push the changes to the main branch:
```
git push -u origin main
```
This is the standard procedure to get started with a Git project and share it with a remote repository.

---
