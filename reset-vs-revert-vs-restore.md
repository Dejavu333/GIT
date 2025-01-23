
![revert-vs-reset](https://github.com/user-attachments/assets/494f2235-0135-42b2-ba62-cba409a20965)

# `git reset` vs `git revert` vs `git restore`

Understanding the differences between `git reset`, `git revert`, and `git restore` is essential to mastering Git. These commands help you undo changes in your repository, but they operate differently and serve different purposes. Let's dive into each one.

## **`git reset`**

The `git reset` command is used to undo changes in the staging area or even in the commit history itself. It moves the `HEAD` pointer (and optionally the index and working directory) to a previous commit. It can be used to unstage changes or delete commits.

### **Key Features of `git reset`:**
- **Affects the `HEAD` and Staging Area**: It can move the `HEAD` to a specific commit and reset the staging area accordingly.
- **Three Modes**:
  - **`--soft`**: Moves the `HEAD` but keeps the changes in the staging area.
  - **`--mixed`** (default mode): Moves the `HEAD` and unstages the changes (keeps changes in the working directory).
  - **`--hard`**: Moves the `HEAD`, unstages the changes, and clears the working directory, effectively discarding any uncommitted changes.

### **Example Usage:**
1. **`git reset --soft HEAD~1`**:  
   - Moves `HEAD` back by one commit but keeps the changes staged for the next commit.
   
2. **`git reset --mixed HEAD~1`**:  
   - Moves `HEAD` back by one commit and unstages the changes, but keeps them in the working directory.
   
3. **`git reset --hard HEAD~1`**:  
   - Moves `HEAD` back by one commit and clears the staging area and working directory, discarding all changes.

### **When to Use `git reset`:**
- Undo commits or changes in the staging area.
- Unstage files or discard local changes in the working directory.
- **Be cautious** when using `--hard` as it can permanently delete changes.

---

## **`git revert`**

Unlike `git reset`, `git revert` is a safer operation. It is used to undo a commit by creating a new commit that reverses the changes made in a specific commit. This does not modify the commit history and is useful for undoing changes in a shared repository.

### **Key Features of `git revert`:**
- **Creates a New Commit**: Unlike `git reset`, `git revert` does not alter the commit history. Instead, it generates a new commit that undoes the changes made by the previous commit.
- **Safe for Shared Repositories**: Since it doesn't change the history, it's safe to use in shared or public branches.

### **Example Usage:**
1. **`git revert [commit_hash]`**:  
   - Creates a new commit that undoes the changes made by the specified commit.
   
2. **`git revert --no-commit [commit_hash]`**:  
   - Reverts the commit but does not commit the changes automatically, allowing you to review or modify them before committing.

### **When to Use `git revert`:**
- Undo a commit without affecting the commit history.
- Revert a change in a shared or public branch.
- If you need to undo a commit but still keep track of the reversal.

---
