# Git_Training_Guide
Git_Training_Guide selfmade for future references


# 🚀 Git & Version Control — Complete Training Guide
> **From Zero to Job-Ready** | Trained by Senior DevOps Engineer  
> Author: Vivek | Last Updated: 2025

---

## 📋 Table of Contents

1. [Module 1 — Fundamentals](#module-1--fundamentals)
2. [Phase 1 — Git Basics](#phase-1--git-basics)
3. [Phase 2 — Branching](#phase-2--branching)
4. [Phase 3 — Remote Repositories](#phase-3--remote-repositories)
5. [Phase 4 — Advanced Git](#phase-4--advanced-git)
6. [Phase 5 — Real-World Workflows](#phase-5--real-world-workflows)
7. [Interview Preparation](#-interview-preparation)
8. [Quick Command Reference](#-quick-command-reference)
9. [Common Mistakes to Avoid](#-common-mistakes-to-avoid)

---

## Module 1 — Fundamentals

### What is Version Control?

Version Control is a system that records changes to files over time so you can recall specific versions later.

**Without Git (Bad way):**
```
report_v1.docx
report_v2.docx
report_final.docx
report_final_ACTUAL.docx      ← chaos!
```

**With Git:** Every change is tracked automatically with who, what, when, and why.

---

### What is Git?

Git is a **Distributed Version Control System (DVCS)** created by **Linus Torvalds in 2005**.

**DVCS Architecture:**
```
Developer A          Developer B          Developer C
[Full Repo Copy] ←→ [Full Repo Copy] ←→ [Full Repo Copy]
       ↕                   ↕                   ↕
              [GitHub — Central Remote Repo]
```

Every developer has a **complete copy** of the entire project history locally.

---

### Git vs GitHub

| | Git | GitHub |
|---|---|---|
| **What is it?** | A tool (software) | A website/platform |
| **Where does it live?** | Your computer (local) | Internet (cloud) |
| **Who made it?** | Linus Torvalds | Microsoft (acquired 2018) |
| **Can it work alone?** | ✅ Yes | ❌ No (needs Git) |
| **Purpose** | Track changes locally | Host repos, collaborate online |
| **Alternatives** | — | GitLab, Bitbucket, Azure DevOps |

> 💡 **Analogy:** Git = Microsoft Word (software). GitHub = Google Drive (cloud storage/sharing).

---

### Why Companies Use Git

| Reason | What It Means in Practice |
|---|---|
| **Collaboration** | 100s of devs work on same codebase without stepping on each other |
| **History** | Every change is logged — who, what, when, why |
| **Rollback** | Revert to a stable version in seconds |
| **Branching** | Features built in isolation, merged only when ready |
| **Code Review** | PRs ensure quality before merging |
| **CI/CD Integration** | Git triggers automated builds, tests, deployments |

---

### Module 1 — Quiz & Correct Answers

**Q1. What is the difference between Git and GitHub?**

✅ **Answer:** Git is a version control tool installed on your local machine to track code changes. GitHub is a cloud-based platform that hosts Git repositories online, enabling team collaboration. Git can work without GitHub, but GitHub cannot work without Git.

---

**Q2. Why is Git called a Distributed Version Control System?**

✅ **Answer:** In DVCS, every developer has a full copy of the entire repository on their local machine. Unlike centralized systems (CVCS), if the central server goes down, work can continue because every developer has the full history. You can also commit, view history, and work offline.

---

**Q3. Why would a team use branches instead of committing directly to main?**

✅ **Answer:** Branches allow multiple developers to work on different features simultaneously without interfering with each other. Each feature/bug fix lives in its own branch, gets reviewed and tested, then merged into main only when stable — keeping main always production-ready. This enforces a code review gate before anything touches production.

---

## Phase 1 — Git Basics

### The Git File Lifecycle

```
┌─────────────┐    git add     ┌─────────────┐   git commit  ┌─────────────┐
│  UNTRACKED  │ ─────────────► │   STAGED    │ ────────────► │  COMMITTED  │
│  (new file) │                │ (ready to   │               │ (saved in   │
│             │                │  snapshot)  │               │  history)   │
└─────────────┘                └─────────────┘               └─────────────┘
```

> 💡 **Analogy:** Untracked = person walks into photo studio. `git add` = pose them in front of camera (staged). `git commit` = take the photo (permanent snapshot).

---

### Core Git Commands

```bash
git init                        # Initialize a new Git repository
git clone <url>                 # Copy a remote repository locally
git status                      # Check staged/untracked/modified files
git add filename.txt            # Stage one file
git add .                       # Stage ALL changed files
git commit -m "message"         # Save snapshot with message
git log                         # View full history
git log --oneline               # Compact history view (used daily)
git log --oneline --graph       # Visual branch graph
```

---

### Commit Message Standards

| ❌ Bad | ✅ Good |
|---|---|
| `"changes"` | `"Fix null pointer in login validation"` |
| `"done"` | `"Add responsive navbar for mobile view"` |
| `"asdfgh"` | `"Refactor payment module to reduce latency"` |

**Rule:** `<verb> <what> <why if needed>`  
**Verbs to use:** Add, Fix, Update, Remove, Refactor, Improve

---

### Phase 1 — Quiz & Correct Answers

**Q1. What is the difference between `git add` and `git commit`? Why two steps?**

✅ **Answer:** `git add` moves changes to the staging area — like putting items in a box. `git commit` seals and labels that box permanently. Two steps give us precise control: you might change 5 files but only want to commit 2. Staging lets you choose exactly what goes into each snapshot.

---

**Q2. What command shows which files are staged vs untracked?**

✅ **Answer:** `git status`
- Red files = modified/untracked (not staged)
- Green files = staged (ready to commit)
- Clean message = nothing to commit

---

**Q3. What's wrong with `git commit -m "fixed stuff"`?**

✅ **Answer:** It's vague — another developer reading it later has no idea what was fixed or why. Better: `git commit -m "Fix login page crash when password field is empty"` — starts with action verb, describes what and why.

---

### Phase 1 — Practical Task: Correct Solution

```bash
# 1. Initialize repository
git init

# 2. Check status
git status

# 3. Stage only index.html
git add index.html

# 4. Commit with professional message
git commit -m "Add index.html with base homepage structure"

# 5. Stage and commit style.css separately
git add style.css
git commit -m "Add style.css with responsive layout styling"
```

---

## Phase 2 — Branching

### What is a Branch?

A branch is a **lightweight movable pointer to a specific commit** — NOT a copy of the project.

```
# After creating feature branch:
A ──► B ──► C ──► D
                  ▲         ▲
                main    feature-login

# After committing on feature-login:
A ──► B ──► C ──► D ──► E ──► F
                  ▲              ▲
                main        feature-login
```

`main` is untouched. Feature lives separately until merged.

---

### What is HEAD?

`HEAD` = pointer to the branch you're currently on.

```bash
git switch feature-login
# HEAD now points to feature-login
# Files change to reflect that branch's state
```

---

### Core Branching Commands

```bash
git branch feature-login            # Create a branch
git switch feature-login            # Switch to branch (modern)
git checkout feature-login          # Switch to branch (old way, still works)

git switch -c feature-login         # Create AND switch (most used) ✅
git checkout -b feature-login       # Same, old syntax

git branch                          # List local branches
git branch -a                       # List local + remote branches

git switch main
git merge feature-login             # Merge feature into main

git branch -d feature-login         # Safe delete (only if merged) ✅
git branch -D feature-login         # Force delete (even if unmerged) ⚠️
```

---

### Branch Naming Convention

```bash
feature/user-authentication         # New features
bugfix/login-null-pointer           # Bug fixes
hotfix/payment-crash-prod           # Urgent production fixes
release/v2.1.0                      # Release branches
```

---

### Merge Conflicts

Happens when two branches modify the **same line** of the same file differently.

```
<<<<<<< HEAD (your current branch)
name = "Raj"
=======
name = "Kumar"
>>>>>>> feature-login (incoming branch)
```

**Resolution steps:**
```bash
# 1. Open the file, manually choose what to keep
# 2. Remove all conflict markers (<<<<<<, =======, >>>>>>>)
# 3. Stage the resolved file
git add filename.py
# 4. Complete the merge
git commit -m "Resolve merge conflict in user name field"
```

---

### Phase 2 — Quiz & Correct Answers

**Q1. What is a branch? Why is it NOT a copy?**

✅ **Answer:** A branch is a lightweight movable pointer to a specific commit. It's not a copy because Git doesn't duplicate files — it just creates a new pointer. This is why creating a branch is instant and costs almost no disk space, even in large projects.

---

**Q2. What does HEAD mean? What happens when you run `git switch feature-login`?**

✅ **Answer:** HEAD is a special pointer that tells Git which branch I'm currently working on. When I run `git switch feature-login`, HEAD moves from main to feature-login — so all new commits now go onto that branch.

---

**Q3. What is a merge conflict and how do you resolve it?**

✅ **Answer:** A merge conflict occurs when two branches modify the same line of the same file differently, and Git cannot automatically decide which version to keep. Git pauses the merge and marks the conflict in the file with `<<<<<<<`, `=======`, and `>>>>>>>` markers. The developer manually edits the file to resolve it, then runs `git add` and `git commit` to complete the merge.

---

### Phase 2 — Practical Task: Correct Solution

```bash
# 1. Update main before starting
git switch main
git pull

# 2. Create and switch to Task A branch
git switch -c feature/product-search

# 3. Simulate work and commit on Task A
touch search.py
git add search.py
git commit -m "Add product search functionality"

# 4. Switch back to main, create Task B branch
git switch main
git switch -c bugfix/add-to-cart

# 5. Simulate fix and commit on Task B
touch cart.py
git add cart.py
git commit -m "Fix broken Add to Cart button logic"

# 6. Merge Task B fix into main (be ON main first!)
git switch main
git merge bugfix/add-to-cart

# 7. Safe delete Task B branch
git branch -d bugfix/add-to-cart
```

> ⚠️ **Merge direction rule:** You must be ON the branch that RECEIVES changes. Name the branch that GIVES changes.
> ```
> git switch main               ← I am here (receiver)
> git merge bugfix/add-to-cart  ← bring this in (giver)
> ```

---

## Phase 3 — Remote Repositories

### Local vs Remote

```
YOUR MACHINE                    GITHUB (Internet)
─────────────────               ──────────────────
[Local Repository]   ────────►  [Remote Repository]
                      git push
                     ◄────────
                      git pull / git fetch
```

---

### Core Remote Commands

```bash
git push origin main                     # Push main to remote
git push -u origin feature/login         # First push (sets upstream tracking)
git push origin feature/product-search  # Push a feature branch

git pull                                 # Fetch + merge (auto)
git pull origin main                     # Explicitly pull main

git fetch origin                         # Download only, DON'T merge
git fetch origin main                    # Fetch specific branch

git remote -v                            # See all configured remotes
git remote add origin <url>             # Add a remote
git remote rename oldname newname       # Rename a remote
```

---

### fetch vs pull vs push

| Command | Downloads? | Merges into local? | When to use |
|---|---|---|---|
| `git fetch` | ✅ Yes | ❌ No | Check what changed before merging |
| `git pull` | ✅ Yes | ✅ Yes (auto) | Daily sync with team |
| `git push` | Uploads ↑ | N/A | Share your commits |

> 💡 **Fetch analogy:** Checking your mailbox — you see new mail arrived, but haven't opened/acted on it yet.

---

### What is `origin`?

`origin` = the default nickname Git gives to your remote repository URL when you clone.

```bash
git remote -v
# origin  https://github.com/username/repo.git (fetch)
# origin  https://github.com/username/repo.git (push)
```

`origin` is just a name — can be changed, but nobody ever does. It's a universal convention.

**Breakdown of `git push origin main`:**
- `git push` = send commits up
- `origin` = destination remote (the nickname)
- `main` = which branch to push to

---

### .gitignore — Always Include This

```bash
# .gitignore
node_modules/       # Dependencies (huge folder)
.env                # Environment variables (passwords, API keys!) ⚠️
*.log               # Log files
__pycache__/        # Python cache
.DS_Store           # Mac system files
```

> ⚠️ **Critical:** API keys pushed to GitHub = security breach. Always `.gitignore` sensitive files BEFORE first commit.

---

### Common Remote Error — Fix Guide

```bash
# Error: fatal: 'origin' does not appear to be a git repository
# Diagnosis:
git remote -v        # Check what remotes exist

# Fix — if origin missing:
git remote add origin https://github.com/username/repo.git

# Fix — if typo in remote name (e.g., "orgin" instead of "origin"):
git remote rename orgin origin

# Verify fix:
git remote -v
git push -u origin main
```

---

### Phase 3 — Quiz & Correct Answers

**Q1. Difference between `git fetch` and `git pull`? When use fetch?**

✅ **Answer:** `git fetch` downloads changes from remote but does NOT merge them into your local branch — like checking your mailbox without opening letters. `git pull` fetches AND automatically merges. Use fetch when you want to review what teammates pushed before deciding to merge — safer in large teams where main changes frequently.

---

**Q2. What does `origin` mean? Can it be changed?**

✅ **Answer:** `origin` is the default nickname Git gives to the remote repository URL when you clone. `git push origin main` means: push my commits to the remote named 'origin' into the branch called 'main'. Yes, it can be renamed with `git remote rename`, but origin is a universal convention — changing it is rare.

---

**Q3. Why should you never push directly to `main`?**

✅ **Answer:** `main` is the production branch — what's on main is what users see live. Pushing broken code directly crashes the product for real users. Feature branches ensure code is reviewed, tested, and approved before touching main. In real companies, this is enforced by **branch protection rules** on GitHub that literally prevent direct pushes to main.

---

### Phase 3 — Practical Task: Correct Solution

```bash
# 1. Clone the team repository
git clone https://github.com/devteam/ecommerce-app.git
cd ecommerce-app

# 2. Make sure you're on main and up to date
git switch main
git pull

# 3. Create feature branch
git switch -c feature/checkout-page

# 4. Create file, stage, commit with good message
touch checkout.html
git add checkout.html
git commit -m "Add checkout page with order summary layout"

# 5. Push branch to GitHub (first time = use -u flag)
git push -u origin feature/checkout-page

# 6. After PR is merged on GitHub → sync local main
git switch main
git pull

# 7. Delete local feature branch (safe delete)
git branch -d feature/checkout-page
```

> 💡 **Key insight:** The PR merge happens on GitHub's interface. Locally you just sync with `git pull` after.

---

## Phase 4 — Advanced Git

### `git stash` — Shelve Work Temporarily

```bash
git stash                            # Stash all uncommitted changes
git stash save "WIP: login page"     # Stash with a label ✅ best practice
git stash list                       # See all stashes
git stash pop                        # Restore latest stash + delete it
git stash pop stash@{0}              # Restore by index
git stash apply                      # Restore but KEEP in stash list
git stash drop                       # Delete a stash permanently
```

> 💡 **Analogy:** You're cooking dinner (coding), emergency call comes in. Put everything in fridge (stash), handle emergency, come back and take it out exactly as you left it (pop).

**Real workflow:**
```bash
git stash save "WIP: user profile page"   # shelve half-done work
git switch main
git pull
git switch -c hotfix/login-crash
# fix bug...
git add . && git commit -m "Fix null reference in login"
git switch feature/user-profile
git stash pop                              # restore your work
```

---

### `git merge` vs `git rebase`

#### git merge — Preserves full history
```bash
git switch main
git merge feature/login
# Creates a merge commit — full history preserved
```
```
A──B──C──────────M   ← merge commit
         \      /
          D──E──
```
✅ Safe, non-destructive  
✅ Full history preserved  
⚠️ History can look messy with many branches

#### git rebase — Clean linear history
```bash
git switch feature/login
git rebase main
# Replays commits on top of main
```
```
A──B──C──D'──E'   ← clean linear history
```
✅ Clean, readable history  
⚠️ **Never rebase shared/public branches!**

#### Golden Rule
```
merge  → safe, use for shared branches (main, develop)
rebase → clean history, use on YOUR local feature branches ONLY
```

> ⚠️ **Why not rebase shared branches?** Rebase **rewrites commit IDs (SHA hashes)**. Teammates still have the old hashes — their repos think histories have diverged. They'll get conflicts on every pull.

---

### `git cherry-pick` — Apply One Specific Commit

```bash
git cherry-pick a3f2c1d         # Apply specific commit to current branch
```

**Real use case:**
```
feature/payments branch commits:
  a1b2c3 — Add Stripe integration
  d4e5f6 — Fix typo in button       ← you only want THIS one
  g7h8i9 — Add PayPal (not ready)

git switch main
git cherry-pick d4e5f6            # Only the typo fix goes to main
```

---

### Undoing Things — `reset` vs `revert`

```bash
git reset --soft HEAD~1     # Undo commit, KEEP changes STAGED     ← safest
git reset --mixed HEAD~1    # Undo commit, changes go UNSTAGED      ← default
git reset --hard HEAD~1     # Undo commit, DESTROY changes forever  ← DANGEROUS ⚠️

git revert HEAD             # Create new undo commit (safe for pushed code) ✅
```

| | `git reset` | `git revert` |
|---|---|---|
| What it does | Moves branch pointer back | Creates a new undo commit |
| History | Erases commits | Preserves all history |
| Safe for pushed code? | ❌ Never | ✅ Always |
| Use case | Local cleanup only | Undoing on main/shared branch |

---

### Phase 4 — Quiz & Correct Answers

**Q1. You're halfway through coding a feature. Manager says fix urgent bug NOW. What do you do?**

✅ **Answer:** Use `git stash save "WIP: feature description"` to temporarily shelve the incomplete work without committing it. Then switch to main, create a hotfix branch, fix the bug, commit and push. Then switch back to the feature branch and restore work with `git stash pop`. I stash instead of committing because half-done code shouldn't pollute commit history.

---

**Q2. Difference between `git reset --soft` and `git reset --hard`? Which is dangerous?**

✅ **Answer:**
- `--soft` → undoes the commit but keeps changes **staged** (safest)
- `--mixed` → undoes the commit, changes go **unstaged** (default)
- `--hard` → undoes the commit AND **destroys changes permanently** (dangerous ⚠️)

`--hard` is dangerous because deleted changes cannot be recovered.

---

**Q3. Why should you NEVER rebase `main` or any shared branch?**

✅ **Answer:** Rebase rewrites commit IDs (SHA hashes). If I rebase main, all existing commits get new hashes. My teammates' local repos still have the old hashes — Git thinks the histories have diverged completely, causing conflicts on every pull. The golden rule: **never rebase any branch others are working on.**

---

### Phase 4 — Practical Task: Correct Solution

```bash
# 1. Stash current work with label
git stash save "half done feature/dashboard"

# 2. Switch to main and pull latest (always pull before branching!)
git switch main
git pull

# 3. Create hotfix branch and fix the bug
git switch -c hotfix/navbar-crash
# edit the broken file...
git add .
git commit -m "Fix navbar crash caused by null ref on mobile"

# 4. Merge hotfix INTO main (be ON main first!)
git switch main
git merge hotfix/navbar-crash

# 5. Return to feature branch and restore stashed work
git switch feature/dashboard
git stash list                    # find stash index
git stash pop stash@{0}           # restore work

# 6. Undo last commit, keep changes staged (to fix commit message)
git reset --soft HEAD~1

# 7. Recommit with better message
git commit -m "Add admin and user dashboard with role-based layout"
```

---

## Phase 5 — Real-World Workflows

### GitHub Flow (Industry Standard)

```
main (always production-ready, PROTECTED)
    │
    ├──► feature/user-auth         ← Developer 1
    ├──► feature/payment-gateway   ← Developer 2
    ├──► bugfix/otp-timeout        ← Developer 3
    └──► hotfix/crash-prod         ← Senior Dev (urgent)
```

### Pull Request Lifecycle

```
1. Developer pushes feature branch to GitHub
2. Opens PR with clear description
3. Assigns reviewers (senior devs / teammates)
4. Reviewers comment, request changes
5. Developer fixes, pushes again (PR auto-updates)
6. Reviewer approves ✅
7. CI/CD pipeline runs (automated tests pass)
8. Merge into main ✅
9. Feature branch deleted
10. Feature live in production 🚀
```

### Branch Protection Rules (Real GitHub Settings)

```
✅ Require pull request before merging
✅ Require at least 1 reviewer approval
✅ Require CI/CD checks to pass
✅ Restrict who can push to main directly
```

---

### Developer's Daily Git Workflow

```bash
# ☀️ START OF DAY
git switch main
git pull                              # sync with team's overnight work
git switch feature/my-task
git rebase main                       # put my branch on top of latest main

# 💻 DURING THE DAY (repeat)
# write code...
git add .
git status                            # always check before committing
git commit -m "Add validation logic for OTP input"

# 🌙 END OF DAY
git push origin feature/my-task      # backup work to GitHub
```

---

### Agile Sprint Git Workflow

```
SPRINT (2-week cycle):
─────────────────────────────────────────
Monday W1    → Sprint planning → tickets assigned → branches created
Tue-Thu W1   → Feature development on branches, daily commits
Friday W1    → PRs opened, code reviews begin

Mon-Tue W2   → Review feedback addressed, PRs updated
Wednesday W2 → PRs approved, features merged to main
Thursday W2  → QA testing on staging environment
Friday W2    → Release to production 🚀, sprint retrospective
```

---

### What Companies Expect From Freshers on Day 1

| Expectation | Details |
|---|---|
| Never push directly to `main` | Always branch → PR → merge |
| Meaningful commit messages | Action verb, clear description |
| Pull before you push | Always sync first |
| Small, focused commits | One feature/fix per commit |
| Respond to PR reviews promptly | Fix and re-push within 24hrs |
| Delete branches after merge | Keep repo clean |
| Use `.gitignore` | Never commit secrets or `node_modules` |

---

### Phase 5 — Final Practical Task: Correct Solution

```bash
# ☀️ 1. START OF DAY SYNC
git switch main
git pull

# 🌿 2. CREATE PROPERLY NAMED FEATURE BRANCH
git switch -c feature/transaction-history

# 💻 3. THREE MEANINGFUL COMMITS (3 stages of work)
touch transaction-history.html
git add transaction-history.html
git commit -m "Add transaction history page with base layout"

touch transaction-api.js
git add transaction-api.js
git commit -m "Add API integration to fetch user transactions"

touch transaction.css
git add transaction.css
git commit -m "Add responsive styles for transaction history table"

# 🚨 4. URGENT BUG — stash, fix, come back
git stash save "WIP: transaction history feature"

git switch main
git pull
git switch -c hotfix/payment-button-crash
# fix bug...
git add .
git commit -m "Fix payment button crash on iOS Safari"
git switch main
git merge hotfix/payment-button-crash
git branch -d hotfix/payment-button-crash

git switch feature/transaction-history
git stash pop stash@{0}

# 📤 5. PUSH FEATURE BRANCH (PR READY)
git push -u origin feature/transaction-history
# → Open PR on GitHub with description, assign reviewers

# 🔄 6. AFTER PR MERGED — CLEAN UP
git switch main
git pull                              # sync the merged changes
git branch -d feature/transaction-history   # delete local branch
```

---

## 🎯 Interview Preparation

### Tier 1 — Every Fresher Gets Asked These

**Q: What is the difference between `git merge` and `git rebase`?**

✅ **Answer:** Both integrate changes from one branch to another. Merge preserves full history and creates a merge commit — safe for shared branches. Rebase replays commits on top of another branch creating a linear history — only use on local feature branches, never on shared ones as it rewrites commit IDs (SHA hashes) which breaks teammates' repos.

---

**Q: How do you resolve a merge conflict?**

✅ **Answer:** Git marks conflicting sections with `<<<<<<<`, `=======`, `>>>>>>>` markers. I open the file, manually choose which code to keep, remove all markers, then run `git add` on the resolved file and `git commit` to complete the merge.

---

**Q: What is HEAD in Git?**

✅ **Answer:** HEAD is a special pointer indicating the currently checked-out branch or commit. When I switch branches with `git switch`, HEAD moves with me to point to the new branch.

---

**Q: What is `git stash` and when would you use it?**

✅ **Answer:** `git stash` temporarily shelves uncommitted changes so I can switch context (e.g., fix an urgent bug) without committing half-done work. I use `git stash save "description"` to label it, and `git stash pop` to restore it later. I use it instead of committing because incomplete code shouldn't pollute commit history.

---

**Q: Difference between `git reset` and `git revert`?**

✅ **Answer:** `git reset` moves the branch pointer back, effectively erasing commits — never use on pushed/shared code. `git revert` creates a new commit that undoes the changes, preserving full history — this is safe for shared branches because it doesn't rewrite history.

---

**Q: What is a Pull Request?**

✅ **Answer:** A PR is a formal request to merge your feature branch into main, with a built-in code review process. Team members review the code, suggest changes, and approve before merging. It's the quality gate that ensures broken code never reaches production.

---

### Tier 2 — Scenario-Based Questions

**Q: You accidentally committed a password to main and pushed it. What do you do?**

✅ **Answer:** First, **immediately invalidate the password/API key** — assume it's compromised the moment it's pushed. Then use `git revert HEAD` to create an undo commit and push it. Never use `git reset` on pushed commits as it rewrites history. Inform the team immediately. Going forward, use `.gitignore` and environment variables to prevent this.

---

**Q: Your feature branch is 2 weeks old and far behind main. How do you sync it?**

✅ **Answer:** 
```bash
git fetch origin
git rebase origin/main           # replay my commits on top of latest main
# resolve any conflicts...
git push --force-with-lease      # update remote branch safely
```
I use `--force-with-lease` instead of `--force` because it's safer — it only force-pushes if nobody else has pushed to the branch since my last fetch.

---

**Q: What is the difference between `git fetch` and `git pull`?**

✅ **Answer:** `git fetch` downloads changes from remote but does NOT merge them — you can inspect them first. `git pull` is essentially `git fetch` + `git merge` in one command. In large teams, `git fetch` followed by manual merge/rebase gives more control and is safer.

---

## 📚 Quick Command Reference

### Setup
```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git init                                    # New local repo
git clone <url>                             # Clone remote repo
```

### Daily Commands
```bash
git status                                  # Check state
git add .                                   # Stage all
git add <file>                              # Stage specific file
git commit -m "message"                     # Commit
git push origin <branch>                    # Push
git pull                                    # Pull + merge
```

### Branching
```bash
git switch -c <branch>                      # Create + switch
git switch <branch>                         # Switch
git branch                                  # List branches
git merge <branch>                          # Merge into current
git branch -d <branch>                      # Delete (safe)
git branch -D <branch>                      # Delete (force)
```

### Advanced
```bash
git stash save "label"                      # Stash work
git stash pop                               # Restore stash
git stash list                              # See stashes
git rebase main                             # Rebase onto main
git cherry-pick <hash>                      # Apply one commit
git reset --soft HEAD~1                     # Undo commit (keep staged)
git reset --hard HEAD~1                     # Undo commit (destroy) ⚠️
git revert HEAD                             # Safe undo (new commit)
git log --oneline --graph                   # Visual history
git remote -v                               # See remotes
git remote add origin <url>                 # Add remote
git remote rename <old> <new>               # Rename remote
```

---

## ⚠️ Common Mistakes to Avoid

| Mistake | Why It's Wrong | Fix |
|---|---|---|
| Committing directly to `main` | Bypasses review, breaks production | Always use feature branches |
| `git add .` without checking | Accidentally stages passwords/junk | Run `git status` first |
| Vague commit messages like `"changes"` | Nobody knows what changed | Use: `Add/Fix/Update <what> <why>` |
| Not pulling before pushing | Push rejected, conflicts | Always `git pull` first |
| Using `git reset` on pushed commits | Breaks teammates' repos | Use `git revert` instead |
| Rebasing shared branches | Rewrites history, causes conflicts | Only rebase your local branches |
| `git branch -D` after merge | Works but risky habit | Use `-d` (safe delete) by default |
| Forgetting `-u` on first push | Tracking not set up | `git push -u origin branchname` |
| Committing `.env` or API keys | Security breach | Always `.gitignore` sensitive files |
| Not pulling before branching | Branch starts on outdated code | `git pull` then create branch |

---

## 📅 Study Plans

### 1-Day Crash Plan (8 hours)
```
Hour 1-2  → Module 1 + Phase 1 (Fundamentals + Basics)
Hour 3-4  → Phase 2 (Branching — most important topic)
Hour 5    → Phase 3 (Remote Repositories)
Hour 6    → Phase 4 (Advanced Git — stash, reset, revert)
Hour 7    → Phase 5 (Real-world workflows + PRs)
Hour 8    → Interview prep + practice all commands in terminal
```

### 3-Day Structured Plan
```
Day 1: Module 1 → Phase 1 → Phase 2
       Practice: Create repo, commit 5 times, create 3 branches, merge 1

Day 2: Phase 3 → Phase 4
       Practice: Push to GitHub, create PR, practice stash/reset

Day 3: Phase 5 + Interview Prep
       Practice: Full feature branch workflow end-to-end
       Review: All quiz questions + common mistakes
```

---

## 🏆 Training Progress Tracker

| Module | Topic | Score | Status |
|---|---|---|---|
| Module 1 | Fundamentals | 85/100 | ✅ Cleared |
| Phase 1 | Git Basics | 82/100 | ✅ Cleared |
| Phase 2 | Branching | 78/100 | ✅ Cleared |
| Phase 3 | Remote Repositories | 79/100 | ✅ Cleared |
| Phase 4 | Advanced Git | 76/100 | ✅ Cleared |
| Phase 5 | Real-World Workflows | 🔄 In Progress | — |

**Overall: 80/100 — Job Ready Track ✅**

---

## 🔑 Key Phrases for Interviews

Memorize these — they make you sound like an experienced developer:

- *"I never commit directly to main — always a feature branch, PR, and code review"*
- *"git revert is safer than reset for pushed commits because it preserves history"*
- *"rebase rewrites commit IDs — never use it on shared branches"*
- *"I use git stash to shelve incomplete work without polluting commit history"*
- *"main should always be production-ready — that's enforced by branch protection rules"*
- *"fetch downloads, pull fetches + merges — I use fetch when I want to review before merging"*
- *"a good commit message starts with an action verb and explains what and why"*

---

*Document generated from Git Training Program — Senior DevOps Engineer / Git Trainer*  
*Save this file, upload to GitHub, and revisit anytime! 🚀*
