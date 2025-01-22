
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

## **`git restore`**

The `git restore` command was introduced in Git 2.23 as a more intuitive way to undo changes in the working directory and staging area. It focuses on restoring files to their previous state without affecting the commit history.

### **Key Features of `git restore`:**
- **Restores Files in the Working Directory**: It is used to discard changes in the working directory or unstage files that have been added to the staging area.
- **Does Not Modify Commit History**: Unlike `git reset` and `git revert`, `git restore` does not affect the commit history.
- **Can Restore Files from Any Commit**: You can restore a file to a specific commit's version.

### **Example Usage:**
1. **`git restore [file_name]`**:  
   - Discards changes in the specified file and restores it to the state of the last commit.
   
2. **`git restore --staged [file_name]`**:  
   - Unstages the file (removes it from the staging area) but keeps the changes in the working directory.
   
3. **`git restore --source [commit_hash] [file_name]`**:  
   - Restores the specified file to the version in a specific commit.

### **When to Use `git restore`:**
- Discard local changes in the working directory for one or more files.
- Unstage changes without modifying the commit history.
- Restore a file to a specific commit's state without affecting other files.

---

## **Comparison Summary:**

| **Feature**                | **`git reset`**                                      | **`git revert`**                                      | **`git restore`**                                      |
|----------------------------|-----------------------------------------------------|-------------------------------------------------------|-------------------------------------------------------|
| **Main Purpose**            | Resets the repository's state by modifying `HEAD`, the staging area, or working directory. | Reverts a commit by creating a new commit that undoes the previous commit. | Restores files to a previous state in the working directory or staging area. |
| **Affects Commit History**  | Yes, it can modify the commit history. | No, it creates a new commit that undoes previous changes. | No, it does not affect commit history. |
| **Affects Staging Area**    | Yes, it can unstage changes or reset the index. | No, it does not affect the staging area. | Yes, it can unstage changes (using `--staged`). |
| **Affects Working Directory** | Yes, it can modify the working directory (especially with `--hard`). | No, it only creates a commit that undoes changes. | Yes, it can restore files to the state of a previous commit. |
| **Use Case**                | Undo commits, unstage changes, or discard local changes. | Undo a commit safely without affecting the commit history. | Discard local changes in the working directory or unstage files. |
| **Risk Level**              | Can be risky, especially with `--hard`, as it can lose data. | Safe, as it creates a new commit and does not alter history. | Safe, as it does not affect commit history or shared branches. |

---

## **Conclusion:**

- **`git reset`**: A powerful command that alters the commit history and staging area, useful for undoing commits, unstaging changes, or discarding modifications. Be cautious when using `--hard`.
- **`git revert`**: A safer option for undoing commits in a shared repository, as it creates a new commit that undoes the changes, preserving history.
- **`git restore`**: A more intuitive way to discard changes in the working directory or unstage files without modifying commit history.
