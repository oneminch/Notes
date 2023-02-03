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
