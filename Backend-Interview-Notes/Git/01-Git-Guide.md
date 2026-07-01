# 1. Git — Full Guide

> 🟢 **Level:** Beginner | ⭐ **Interview Frequency:** High

---

## 🧠 Concept

**Git** is a **version control system** — it tracks every change to your code, lets many people
work together, and lets you go back to older versions. **GitHub** is a website that hosts Git
repositories online.

---

## 🗺️ The 3 Areas

```
Working Directory → (git add) → Staging Area → (git commit) → Local Repo → (git push) → Remote (GitHub)
   your edits          staged changes            saved history            shared online
```

---

## 🧩 Everyday Commands

```bash
git init                     # start a repo
git clone <url>              # copy a remote repo
git status                   # see what changed
git add .                    # stage all changes
git commit -m "message"      # save a snapshot
git push origin main         # upload to remote
git pull origin main         # download + merge latest
git log --oneline            # view commit history
```

---

## 🌿 Branching & Merging

A **branch** is a separate line of work so you don't break the main code.
```bash
git branch feature-login       # create branch
git checkout feature-login     # switch to it
git checkout -b feature-login  # create + switch (shortcut)
git merge feature-login        # merge branch into current
```

```
main    ●───●───●───────●   (merge)
              \         /
feature        ●───●───●
```

---

## 🔀 Merge vs Rebase

| Merge | Rebase |
|-------|--------|
| Combines branches, keeps history | Moves your commits on top of another branch |
| Creates a merge commit | Linear, cleaner history |
| Safe for shared branches | Don't rebase shared/public branches |

```bash
git merge feature      # keep both histories
git rebase main        # replay my commits on top of main
```

---

## 🛠️ Other Important Commands

| Command | Use |
|---------|-----|
| `git cherry-pick <commit>` | Copy one specific commit to current branch |
| `git stash` / `git stash pop` | Temporarily save uncommitted changes |
| `git reset` | Undo commits (moves branch pointer) |
| `git revert <commit>` | Undo a commit by creating a new opposite commit (safe) |

### Reset vs Revert (common question!)
| Reset | Revert |
|-------|--------|
| Rewrites history (removes commits) | Adds a new commit that undoes |
| Dangerous on shared branches | Safe for shared branches |

```bash
git reset --soft HEAD~1    # undo commit, keep changes staged
git reset --hard HEAD~1    # undo commit + discard changes (careful!)
git revert <commit>        # safely undo a pushed commit
```

---

## 🔄 Pull Request (PR)
A **PR** proposes merging your branch into another (e.g., feature → main). The team **reviews**,
comments, and approves before merging. Core of team collaboration on GitHub.

---

## 🌊 Git Flow (branching strategy)
```
main       → production-ready code
develop    → integration branch
feature/*  → new features
release/*  → prepare a release
hotfix/*   → urgent production fixes
```

---

## 🌍 Real-World Use Case
A team builds features on separate `feature/*` branches, opens PRs for review, merges into
`develop`, then releases to `main`. Git history shows exactly who changed what and when.

---

## ❓ Interview Questions
1. Difference between Git and GitHub?
2. Difference between merge and rebase?
3. Difference between reset and revert?
4. What does `git cherry-pick` do?
5. What is `git stash`?
6. What is a merge conflict? How to resolve it?
7. Difference between `git fetch` and `git pull`? (fetch downloads; pull = fetch + merge)
8. What is a pull request?
9. Explain Git Flow.
10. Difference between `HEAD`, `origin`, and `main`?

---

## ✅ Best Practices
- Write clear commit messages.
- Commit small, logical changes often.
- Never rebase/force-push shared branches.
- Use branches + PRs for every feature.
- Pull latest before starting work.

## ⚠️ Common Mistakes
- `git reset --hard` losing work.
- Committing directly to `main`.
- Force-pushing shared branches.
- Huge commits mixing many changes.

---

## ⚡ Quick Revision Notes
- Flow: edit → `add` → `commit` → `push`.
- Merge keeps history; rebase makes it linear (don't rebase shared branches).
- Reset rewrites history; revert safely undoes with a new commit.
- cherry-pick = grab one commit; stash = shelve changes; PR = reviewed merge.

## 🙋 FAQs
**Q: fetch vs pull?** `fetch` only downloads changes; `pull` downloads **and** merges them.

## 📎 References
- git-scm.com/doc
- GitHub Docs

[⬅ Back to Git Index](./README.md)

