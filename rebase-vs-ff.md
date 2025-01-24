### Fast-Forward Merge (`--ff-only`) vs. Rebase

- **Fast-Forward Merge (`--ff-only`)**:  
  Validates if a fast-forward is possible and creates a linear history without merge commits.  
  - Aborts if a fast-forward isn’t possible.  
  - Ensures no unnecessary merge commits.  
  - Example:  
    ```bash
    git merge --ff-only feature-branch
    ```

- **Rebase**:  
  Creates a linear history regardless of the scenario by "rewriting history."  
  - Removes commits from one place in the history and reinserts them elsewhere.  
  - Fine for unpublished branches but problematic for published ones as it changes commit hashes, causing issues for others.  
  - Example:  
    ```bash
    git rebase main
    ```

> **Key Difference**:  
> `--ff-only` validates and creates a linear history only if possible, while rebase rewrites history to always create a linear structure.

---

### `git merge --ff-only` vs. `git merge`
- **`git merge --ff-only`**:  
  - Aborts if it cannot fast-forward.  
  - Never creates a merge commit.

- **`git merge`**:  
  - Attempts a fast-forward merge if possible.  
  - Creates a merge commit if the branches have diverged.

> Example of `git merge --ff-only`:
```bash
git checkout main
git merge --ff-only feature-branch
```
Aborts if `feature-branch` cannot fast-forward into `main`.

---

### Summary
- Use `--ff-only` to ensure a clean linear history without merge commits.  
- Use **rebase** for creating a linear history by rewriting commits, but avoid on published branches.  
- `git merge` allows for both fast-forward and merge commits, depending on the scenario.
