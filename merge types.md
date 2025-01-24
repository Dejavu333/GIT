![git-merging](https://github.com/user-attachments/assets/7ff87ecc-fe90-47fd-8168-43c0132db4c5)

# Git Merges Guide

## Commit Merge
When development has taken place on both branches before the merge operation, Git has to create a new commit that mixes the changes.

- Git will automatically try to make a commit.
- Using `git merge -n (branch_name)` or having merge conflicts will leave you to make a **manual commit**.

---

## Fast-Forward Merge
If there’s only development in one branch, Git will just update the head position for the receiving branch during the merge.  
The merging branch becomes a subset of the history of the recipient branch.

---

## No Fast-Forward Merge
A special form of a commit merge.  
Using `git merge --no-ff (branch_name)` will **force a commit merge**, even if a fast-forward merge is possible.

---

## Undoing Merges
### Merge Not Pushed Yet
If the merge hasn’t been pushed remotely yet, it’s straightforward to undo:

- For a commit merge that hasn’t been committed yet:  
  ```bash
  git reset HEAD
  ```
  **Warning:**  
  Using `git reset --hard HEAD` will also clear the Working Directory of any changes compared to the HEAD commit.

### Merge Commit Already Made
If the merge commit has already been made, you can move the tip of the receiving branch back to its previous position. For example:

```bash
git checkout master
git reset B
```
This will set the tip of the `master` branch back to commit `B`. The merge commit (`F`) will be ignored and eventually discarded. Replace `B` with the actual SHA of the commit as appropriate.

---

## Undoing Fast-Forward Merges
The process is the same as undoing a regular commit merge:

```bash
git checkout master
git reset B
```
This moves the tip of the `master` branch back to its original position.

