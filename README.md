# Git Cheat Sheet

## Key Git Concepts

### Core Ideas

* **Git** → A distributed version control system for tracking source code history.
* **GitHub** → A cloud-based platform for hosting Git repositories and collaborating.
* **Repository (Local/Remote)** → Local repo exists on your machine; remote repo exists on a server (like GitHub).
* **Version Tracking** → Process of maintaining changes and history of files over time.
* **Branching** → Creating independent lines of development within a project.
* **Staging** → Intermediate area to prepare changes before committing.
* **Working Directory (pwd)** → Current project folder where you edit files.
* **SHA/Hash ID** → Unique identifier assigned to each commit.

### Advanced Ideas

* **Merge Conflicts** → When two branches modify the same part of a file differently.
* **.gitignore** → A file listing patterns of files to exclude from tracking.
* **CI/CD** → Continuous Integration/Continuous Deployment pipelines for automation.
* **Deploying** → Releasing software to production or end-users.
* **gitk** → GUI tool for browsing repository history.

### Ecosystem

* **Open Source** → Software with publicly accessible source code.
* **Open Source Contribution** → Act of collaborating and improving open source projects.
* ([**GitHub Copilot**](https://github.com/features/copilot)) → AI-powered coding assistant by GitHub & OpenAI.
* ([**GitHub Spark**](https://github.blog)) → A modern developer experience platform from GitHub.

---

## Essential Git Commands

### Setup & Config

* `git config --global user.name "<name>"` → Set username.
* `git config --global user.email "<email>"` → Set email.

### Repository Basics

* `git init` → Initialize a new Git repository.
* `git clone <url>` → Clone an existing remote repo.

* `git remote -v` → List configured remote repositories.
* `git remote add origin <link>` → Connect local repository to remote repository.
* `git remote set-url origin <url>` → Change remote URL.

### Staging & Committing

* `git status` → Show changes in working directory vs staging area.

* `git add <file>` → Stage changes for commit.
* `git add .` → Stage all changes.

* `git commit -m "<message>"` → Commit staged changes with a message.
* `git commit -am "<message>"` → Stage and Commit changes in a single command. (files must be tracked)
* `git commit --amend -m "<new message>"` → Modify last commit message/content.

* `echo "node_modules/" >> .gitignore` → Add folder to `.gitignore`.

### Branching & Navigation

* `git branch` → List branches.
* `git branch <branch>` → Create new branch.

* `git switch <branch>` → Switch to branch.
* `git switch -c <branch>` → Create and switch to new branch.

* `git checkout <branch>` → Older way to switch branches.
* `git checkout -b <branch>` → Create and switch to new branch.

### Syncing with Remotes

* `git fetch` → Download latest changes from remote (no merge).
* `git pull` → Fetch + merge remote branch into current branch (fetch + merge).

* `git push origin <branch>` → Push local branch to remote.
* `git push -u origin <branch>` → Push and set upstream (first push).

### Undoing & Cleaning

* `git restore <file>` → Discard changes in working directory.
* `git revert <commit>` → Create new commit that undoes changes from target commit.

* `git reset --soft <commit>` → Move HEAD(un-commit), keep changes staged.
* `git reset --mixed <commit>` → Move HEAD(un-commit), keep changes unstaged (default).
* `git reset --hard <commit>` → Reset completely to older commit (lose changes).

* `git stash` → Save uncommitted changes temporarily.

* `git clean -fd` → Remove untracked files and directories.
* `git rm <file>` → Remove file from repo + staging.
* `git mv <old> <new>` → Rename or move a file.

### Collaboration & Integration

* `git merge <branch>` → Merge another branch into current branch. run on master; <branch> is which branch to merge from.
* `git merge --no-ff <branch>` → Force a merge commit (preserves history).
* `git merge --ff-only <branch>` → Fast-forward only (if there is conflict, cancel merge).
* `git merge --abort` → Cancel merge.

* `git checkout --ours <file>` → Keep current branch’s version in conflict.
* `git checkout --theirs <file>` → Keep incoming branch’s version.
* `git add <file> && git commit` → Finalize resolution *(After manual conflict edits)*.

* `git rebase <branch>` → Reapply commits on top of another branch. run on new branch; <branch> is which branch to merge to.
* `git rebase -i <commit>` → Interactive rebase (edit/squash commits).
* `git rebase --continue` → Continue after fixing conflicts.
* `git rebase --abort` → Cancel rebase.

### Inspecting History

* `git log` → Show commit history.
* `git log --oneline` → Condensed commit history.
* `git log --oneline --graph --decorate --all --date-order` → Pretty graph view.
* `git log --pretty=format:"%h %an %s"` → Custom formatted log.

* `git show <commit>` → Show details of a commit.
* `git show --no-patch --pretty=format:"%h %p %s" HEAD` → Show commit + parent(s) only.

* `git diff` → Show unstaged changes.
* `git diff --staged` → Show staged changes.

* `git blame <file>` → Show who last modified each line of a file.

---

## Typical Git Workflow 

1. **Configure Git (first time only)**

   * `git config --global user.name "<name>"`
   * `git config --global user.email "<email>"`

2. **Start a Project**

   * `git init` *(new repo)* OR `git clone <url>` *(existing repo)*

3. **Create/Move to a Branch**

   * `git switch -c <branch>` *(new branch)*
   * `git switch <branch>` *(existing branch)*

4. **Make Changes**

   * Edit files → `git status` → `git add <file>`

5. **Commit Changes**

   * `git commit -m "<message>"`
   * *(shortcut for tracked files)* `git commit -am "<message>"`

6. **Sync with Remote**

   * First push: `git push -u origin <branch>`
   * Next pushes: `git push`
   * Update from remote: `git pull`

7. **Integrate Work**

   * Merge: `git merge <branch>`
   * Rebase: `git rebase <branch>`
   * Resolve conflicts: edit → `git add <file>` → `git commit`
