# Git Config

## Init

```bash
git init
```

Initialize a git repository

---

## Config Levels

- system
- global
- local

---

## Global Config

```bash
# Set global username and email
git config --global user.name "ashokkumarkola"
git config --global user.email "ashokkumarkola.dev@gmail.com"

# Show global config
git config --global --list
```

---

## Local Config (Repo only)

```bash
# Set global username and email
git config user.name "ashokkumarkola"
git config user.email "newemail@example.com"

# Show local config
git config --local --list
```

---

## View Config

```bash
# Show all active config
git config --list

# Show config source
git config --show-origin user.name
```

---

## Unset

```bash
# Remove local config
git config --unset user.email
```

```bash
# Remove global config
git config --global --unset user.email
```

---

## Aliases

```bash
# Create alias
git config --global alias.i init
```

```bash
# Use alias
git i
```

---
