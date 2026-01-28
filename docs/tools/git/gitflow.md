# GitHub Flow

## Clone

```bash
# Copy remote repo to local
git clone <repo-url>
```

---

## Branch

```bash
# Create and switch to branch
git checkout -b new-branch

# Switch to main branch
git switch main
```

---

## Stage

```bash
# Stage all changes
git add .
```

---

## Commit

```bash
# Save changes locally
git commit -m "message"
```

---

## Push

```bash
# Push branch to remote
git push
```

---

## Pull Request

- Open PR on GitHub
- Review changes
- Merge PR

---

## Delete Branch

```bash
# Delete local branch
git branch -d update-name

# Delete remote branch
git push --delete origin update-name
```

---

## Sync

```bash
# Fetch + merge remote changes
git pull
```

---

## Inspect

```bash
# Show last commit details
git show

# Show unstaged changes
git diff

# Show file changes
git diff commit_id commit_id file
```

---
