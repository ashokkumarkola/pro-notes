# Git SSH Keys — Complete Notes

## Why SSH is needed for GitHub

When you run:

```bash
git push git@github.com:ashokkumarkola/pro-notes.git
```

GitHub needs to verify **who you are**.

It does this using **public-key cryptography**.

GitHub expects:

1. Your computer to prove its identity
2. Using a **private SSH key**
3. That matches a **public SSH key** stored in **your GitHub account**

No username/password is sent.

---

## How SSH authentication works (mental model)

```
Your machine          GitHub
-------------         ----------------
private key   ---->   challenge
             <----   verification
public key    ---->   matched in account
```

- **Private key** → stays on your machine
- **Public key** → uploaded to GitHub
- If they match → access granted

---

## STEP 1: Create an SSH identity (required)

```bash
ssh-keygen -t ed25519 -C "ashokkumarkola.dev@gmail.com"
```

### What each part means

| Part           | Meaning                                       |
| -------------- | --------------------------------------------- |
| `ssh-keygen`   | Tool to generate SSH identities               |
| `-t ed25519`   | Modern, secure algorithm (GitHub recommended) |
| `-C "<email>"` | Comment (label only, not authentication)      |

> The email is just a **human-readable tag**.

---

### Prompts and correct answers

```
Enter file in which to save the key (/home/ashok/.ssh/id_ed25519):
```

✅ **Press Enter**

Why:

- `id_ed25519` is the standard default
- SSH tools automatically look for it
- Avoids custom path issues

```
Enter passphrase (empty for no passphrase):
```

✅ **Press Enter** (empty)

Why:

- Simpler setup
- Passphrases can be added later

---

### Result (important)

You should now have:

```
~/.ssh/id_ed25519        # PRIVATE key (never share)
~/.ssh/id_ed25519.pub    # PUBLIC key (safe to share)
```

This key pair represents your **machine’s identity**.

---

## STEP 2: Load the key into ssh-agent

Your key exists on disk, but SSH will not use it unless it’s loaded.

### Start ssh-agent

```bash
eval "$(ssh-agent -s)"
```

- Starts a background process
- Holds private keys securely in memory

---

### Add the key

```bash
ssh-add ~/.ssh/id_ed25519
```

Expected output:

```
Identity added: /home/ashok/.ssh/id_ed25519
```

---

### If the key was created in the wrong directory

Sometimes keys are accidentally created in the current folder.

Fix:

```bash
mkdir -p ~/.ssh
mv id_ed25519 id_ed25519.pub ~/.ssh/

# Fix permissions (required by SSH)
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_ed25519
chmod 644 ~/.ssh/id_ed25519.pub

# Add key again
ssh-add ~/.ssh/id_ed25519
```

---

## STEP 3: Register the public key with GitHub

GitHub must know your **public key**.

### Copy the public key

```bash
cat ~/.ssh/id_ed25519.pub
```

> Copy the entire output.

---

### Add key to GitHub

1. Log in as **ashokkumarkola**
2. GitHub → **Settings → SSH and GPG keys**
3. Click **New SSH key**

| Field | Value                                  |
| ----- | -------------------------------------- |
| Title | `ThinkPad W530` (any descriptive name) |
| Key   | Paste public key                       |
| Type  | Authentication key                     |

Save.

GitHub now trusts this machine.

---

## STEP 4: Test SSH authentication

```bash
ssh -T git@github.com
```

### Successful output

```
Hi ashokkumarkola! You've successfully authenticated, but GitHub does not provide shell access.
```

This confirms:

- SSH works
- Key is valid
- GitHub recognizes your identity

---

## STEP 5: Push using SSH

```bash
git push -u origin main
```

This time:

- SSH presents your private key
- GitHub matches the public key
- Push succeeds

---

## Why this does NOT affect `gh auth`

| System    | Used for                |
| --------- | ----------------------- |
| `gh auth` | GitHub CLI + HTTPS      |
| SSH keys  | Git operations over SSH |

They are **independent**.

That’s why:

- `gh auth status` may show a different account
- SSH pushes still work correctly

---

## Common files & their roles

| File                    | Purpose              |
| ----------------------- | -------------------- |
| `~/.ssh/id_ed25519`     | Private key (secret) |
| `~/.ssh/id_ed25519.pub` | Public key           |
| GitHub SSH keys         | Trusted identities   |
| `ssh-agent`             | Holds keys in memory |
| `known_hosts`           | Remembers servers    |

---

## Common mistakes to avoid

- ❌ Sharing private key
- ❌ Creating keys outside `~/.ssh`
- ❌ Wrong file permissions
- ❌ Forgetting to add key to GitHub
- ❌ Confusing Git config with authentication

---

## Key takeaway

> **SSH authentication is machine-based, not account-based.**
> GitHub trusts _keys_, not passwords.

Once set up, SSH becomes:

- secure
- fast
- boring (the best kind of reliable)

---
