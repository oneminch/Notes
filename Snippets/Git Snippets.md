## Add an existing local project to GitHub

```bash
git init
git add .
git commit -m "Add existing project files to Git"
git remote add origin <remote github url>
git push -u origin master
```
## Change the commit message of the most recent unpushed change

```bash
git commit --amend -m "New commit message."
```
## Revert to a previous commit

```bash
git reset --hard <short_hash>
```
## Add a new remote

```bash
git remote remove <remote_name>

git remote add <remote_name> <remote_url>
```

## Remove File from Previous Commit

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