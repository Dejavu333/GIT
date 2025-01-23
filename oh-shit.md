
# Oh Shit Git!

## Oh shit, I did something terribly wrong, please tell me git has a magic time machine!?

```bash
git reflog
# You will see a list of everything you've
# done in git, across all branches!
# Each one has an index HEAD@{index}.
# Find the one before you broke everything.
git reset HEAD@{index}
# Magic time machine
```

You can use this to:
- Recover stuff you accidentally deleted
- Remove changes that broke the repo
- Recover after a bad merge
- Go back to a time when things worked

I use `reflog` A LOT. Mega hat tip to the many people who suggested adding it!

---

## Oh shit, I committed and immediately realized I need to make one small change!

```bash
# Make your change
git add . # or add individual files
git commit --amend --no-edit
# Now your last commit contains that change!
# WARNING: Never amend public commits.
```

This usually happens when I commit, then run tests/linters and realize I missed something trivial (like a space after an equals sign). You could also:
- Make the change as a new commit
- Use `git rebase -i` to squash them together  
But this method is way faster.

**Warning**: Never amend commits that have been pushed to a public/shared branch. Only amend commits in your local copy to avoid issues.

---

## Oh shit, I need to change the message on my last commit!

```bash
git commit --amend
# Follow prompts to change the commit message.
```

Stupid commit message formatting requirements.

---

## Oh shit, I accidentally committed something to `master` that should have been on a new branch!

```bash
# Create a new branch from the current state of master
git branch some-new-branch-name
# Remove the last commit from the master branch
git reset HEAD~ --hard
git checkout some-new-branch-name
# Your commit lives in this branch now :)
```

**Note**: If you've already pushed the commit to a public/shared branch, or if you've made other attempts, you might need to use:
```bash
git reset HEAD@{number-of-commits-back}
```

---

## Oh shit, I accidentally committed to the wrong branch!

```bash
# Undo the last commit, but leave the changes available
git reset HEAD~ --soft
git stash
# Move to the correct branch
git checkout name-of-the-correct-branch
git stash pop
git add . # or add individual files
git commit -m "your message here"
# Now your changes are on the correct branch.
```

Some people prefer using `git cherry-pick` for this situation, so feel free to use whichever works for you!

---

## Oh shit, I tried to run a diff but nothing happened!?

```bash
# If you've made changes but diff is empty,
# you probably added your files to staging.
# Use this special flag to view the changes:
git diff --staged
```

File under ¯\\_(ツ)_/¯. (Yes, I know this is a feature, not a bug, but it’s baffling and non-obvious the first time it happens.)

---

## Oh shit, I need to undo a commit from 5 commits ago!

```bash
# Find the commit you need to undo
git log
# Use the arrow keys to scroll up and down in history
# Once you've found your commit, save the hash
git revert [saved hash]
# Git will create a new commit that undoes that commit
# Follow prompts to edit the commit message, or just save and commit
```

You don’t have to copy-paste old file contents manually to undo changes! Use `revert` to undo a commit all in one go.

---

## Oh shit, I need to undo my changes to a file!

```bash
# Find a hash for a commit before the file was changed
git log
# Use the arrow keys to scroll up and down in history
# Once you've found your commit, save the hash
git checkout [saved hash] -- path/to/file
# The old version of the file will be in your index
git commit -m "Wow, you don't have to copy-paste to undo"
```
