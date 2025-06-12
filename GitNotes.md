## **Intro**
---
cat filename -> display file contents  
To remove files from staging area: `git restore --staged <filename or .>`  
To add and commit in one line (only for already staged/tracked files):  
`git commit -a -m "updated Commit"`  
`git clean -n`: Shows which untracked files are there  
`git clean -f`: Deletes the untracked files  

---

## Branch

- `git branch` -> shows all branches  
- `git branch [branchname]` -> create a branch  
- `git branch -b [branchname]` -> create a branch and switch to it  
- `git branch -d [branchname]` -> delete a branch  
- `$ git branch -r` -> shows remote repository branches  
- `$ git branch -a` -> shows all branches  
- `git branch -m <old_name> <new_name>` – Renames a branch  
- `git branch --merged` – Lists branches that have been merged into the current branch  
- `$ git checkout [branchname]` -> switches the current branch to branchname  
- `git diff branchname` -> compares difference between current branch and branchname  
- `git diff branch1 branch2` -> compares difference between branch1 and branch2 irrespective of which branch you're in  
- `git merge branchname` -> merges branchname into current branch  

**To Push branches to Remote repository**  
- `git push AliasNameOfrepository branch1 branch2 branch3 ...`  
- `git push AliasNameOfrepository --all` -> pushes all branches to remote repository (not tags)  

**To Pull branches from Remote repository**  
- `git pull AliasNameOfrepository branch`  

---

## Tag

Git tags are immutable, while branches are mutable.

- `git tag` -> see how many tags are there  
- `git tag tagname` -> create a tag  
- `git push aliasName tag [tagname]`  
- `git push aliasName --tags` -> pushes all tags from local repo to remote repo  

Tags are created when development is done, usually for versioning like `softV1.0.0` to indicate releases.  
Example: `v1(major version).0(minor version).0(patch)`

- `git tag -d [tagname]` -> delete tag in local repository (tags cannot be deleted or modified in remote repo)  

---

## Stash

To create backups in case you need to switch branches in the middle of something without committing your code.

- `git stash` -> creates a backup of the current working directory and reverts changes to the last commit  
- `git stash list` -> lists all stash backups  
- `git stash apply` -> applies the latest stash  
- `git stash apply stash@{n}` -> applies a specific stash  
- `git stash drop` -> deletes the latest stash  
- `git stash drop stash@{n}` -> deletes the mentioned stash  
- `git stash pop` -> applies the latest stash and deletes it  
- `git stash pop stash@{n}` -> applies the mentioned stash and deletes it  

---

## Git Cherry-Pick

Git Cherry-Pick allows you to apply specific commits from one branch to another **without merging** the entire branch.  
This is useful for transferring individual changes like bug fixes or feature updates.

- `git log --oneline` or `git log` -> get the commit IDs/hashes  
- `git cherry-pick [commit id]` -> applies the commit with commit ID to the current branch  

### Usage
```bash
git cherry-pick <commit-hash>
```

This applies the specified commit to the current branch.

### Types of Cherry-Picking
1. Single Commit Cherry-Picking  
   ```
   git cherry-pick abc1234
   ```
   This applies the commit `abc1234` to the current branch.

2. Multiple Commits Cherry-Picking  
   ```
   git cherry-pick abc1234 def5678
   ```
   This applies multiple commits in sequence.

3. Range of Commits Cherry-Picking  
   ```
   git cherry-pick abc1234^..def5678
   ```
   This picks all commits between `abc1234` and `def5678`.

4. Cherry-Picking with Conflict Resolution  
   If conflicts arise, Git will pause the operation. You can resolve conflicts manually and continue:
   ```
   git cherry-pick --continue
   ```
   If needed, you can abort the cherry-pick:
   ```
   git cherry-pick --abort
   ```

### Related Commands
- View Commit History  
  ```
  git log --oneline
  ```
  Helps identify commit hashes for cherry-picking.

- Reverting a Cherry-Picked Commit  
  ```
  git revert <commit-hash>
  ```
  This undoes the cherry-picked commit.

- Cherry-Picking with Original Commit Reference  
  ```
  git cherry-pick -x <commit-hash>
  ```
  Adds a reference to the original commit in the new commit message.

### Example Scenario
Imagine you have two branches: `feature` and `main`. 
A bug fix was committed to `feature`, but you need it in `main` without merging the entire branch.

```
git checkout main
git cherry-pick abc1234
```
This applies the bug fix from `feature` to `main`.
