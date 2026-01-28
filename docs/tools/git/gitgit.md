
git remote add upstream https://github.com/Rishikagandeti/Wave-13-LMS.git


git clone

git status

git add .

git commit -m ""

git push origin main


## STASH
```bash

git stash
git stash clear
git stash apply
git stash drop
git stash list

```


## BRANCHES
```bash

# Create and switch to a new branch
git checkout -b dev
git switch -c dev

git checkout -b feature/your-feature

# Switch to an existing branch
git checkout branch_name
git switch branch_name

# List all branches
git branch

# Rename the current branch
git branch -m new_branch_name

# Delete a branch
# Delete locally:
git branch -d branch_name      # safe delete (only if merged)
git branch -D branch_name      # force delete
# Delete remotely:
git push origin --delete branch_name

# Push a new branch to remote
git push -u origin dev

# Merge a branch into current branch
git merge branch_name


```





git fetch upstream
git merge upstream/main




git pull rebase
git rebase --continue
git rebase --abort
git config --global pull.rebase true


git restore .











