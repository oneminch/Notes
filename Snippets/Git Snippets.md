## Assorted

### Add an existing local project to GitHub

```bash
git init
git add .
git commit -m "Add existing project files to Git"
git remote add origin <remote github url>
git push -u origin master
```

### Restore / Discard Changes in Tracked Files

```bash
git restore <file>
```

### Unstage File from Git

```bash
git restore --staged <file>
```

## Branching

### Delete a Local Branch

```bash
git branch -d <branch_name>
```

### Delete a Remote Branch

```bash
git push origin --delete <branch_name>
```

## Commits

### Add new file / changes to a previous commit

```bash
# After Making Edits
git add <file>

git commit --amend --no-edit
```

### Change the commit message of the most recent unpushed change

```bash
git commit --amend -m "New commit message."
```

### Revert to a previous commit

```bash
git reset --hard <short_hash>
```

### Remove File from Previous Commit

```bash
git reset --soft HEAD^ 
# OR git reset --soft HEAD~1 

# Old Way
git reset HEAD path/to/file

# New Way
git restore --staged path/to/file

# Reuse Commit (or use new one)
git commit -c ORIG_HEAD
```

### Save Uncommitted Changes and Revert to Last Commit

```bash
git stash

# Include Untracked Files
git stash -u

# With Message
git stash save "Message"

# List all Stashes
git stash list

# Apply & then Remove Most Recent Stash
git stash pop

# Apply a Stash without Removing it
git stash apply stash@{n}

# Delete a Stash
git stash drop stash@{n}

# Delete all Stashes
git stash clear
```

## Remote

### Add a new remote

```bash
git remote remove <remote_name>

git remote add <remote_name> <remote_url>
```

### Get Current Remote URL

```bash
git remote get-url <remote_name>
# e.g. git remote get-url origin
```
