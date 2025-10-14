# git-playground

# Git History & Rebase Lesson

This repository was created as a **Git playground** to practice and understand advanced Git concepts — particularly how to safely **change history** and how **Git pointers and branches** actually work behind the scenes.

---

## What I Learned

### 1. Changing Git History

I learned that Git allows us to **modify commits** to fix mistakes, organize work, or clean up commit messages before pushing changes.
Some useful commands include:

* **`git commit --amend`** → Modify the most recent commit (e.g., add missing files or fix commit messages).
* **`git rebase -i HEAD~n`** → Interactively edit, reorder, rename, squash, or delete past commits.
* **`git rebase --continue`** → Resume a rebase after making changes.

> Important: These history-changing commands should only be used on **local commits** that haven’t been pushed to a shared remote. Changing public history can cause conflicts for collaborators.

---

### 2. Squashing Commits

I learned how to **combine multiple commits into one** using `git rebase -i` and changing the command from `pick` to `squash`.
This helps maintain a **cleaner commit history** by merging small or unnecessary commits together before merging branches.

Example:

```bash
pick e30ff48 Create first file
squash 92aa6f3 Create second file
pick 05e5413 Create third file and create fourth file
```

becomes a single commit: `Create first and second file`.

---

### 3. Splitting a Commit

Using `git reset HEAD~`, I learned how to **undo a commit** and separate its contents into smaller, more meaningful commits.

Example:

```bash
git reset HEAD~
git add test3.md && git commit -m "Create third file"
git add test4.md && git commit -m "Create fourth file"
```

This technique is useful when one commit contains unrelated or mixed changes.

---

### 4. Understanding `git reset`

The `git reset` command can modify the current branch pointer (`HEAD`) and optionally affect the **staging area** and **working directory**.

* `git reset --soft` → Moves HEAD but keeps staged changes.
* `git reset` (default/mixed) → Moves HEAD and unstages files, but keeps working directory changes.
* `git reset --hard` → Moves HEAD and discards all uncommitted changes.

> `--hard` is destructive — it permanently deletes uncommitted work.

---

### 5. Git Pointers & Branches

This was one of the most eye-opening parts of the lesson. I learned that:

* A **branch** is **not a collection of commits** — it’s simply a **pointer** to a single commit.
* Each **commit** also points to the commit before it, forming a **chain** of snapshots.
* **HEAD** is a special pointer that indicates **where you currently are** in your repository.

Example:

```
HEAD → main → Commit D → Commit C → Commit B → Commit A
```

Each commit “points back” to the one before it, which is how Git tracks history.

---

### 6. Best Practices

* Never rebase or amend commits that are already pushed to a shared remote.
* Use **amend** or **interactive rebase** only for **local cleanup**.
* Always communicate with teammates before rewriting shared history.
* Use **squash** to keep your project history neat and meaningful.

---

## Commands Practiced

```bash
touch test{1..4}.md
git add test1.md && git commit -m "Create first file"
git add test2.md && git commit -m "Create send file"
git add test3.md && git commit -m "Create third file and create fourth file"

git add test4.md
git commit --amend
git rebase -i HEAD~2
git rebase --continue
git rebase -i --root
git reset HEAD~
git reset --soft
git reset --hard
```

## Summary

This exercise deepened my understanding of how Git actually works behind the scenes. I now have a solid grasp of how commits, branches, and pointers interact — and how to safely manipulate history to keep my repositories clean, organized, and professional.
