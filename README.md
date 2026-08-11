# Git Guide to Work

> *Based on the principles of Pro Git (Version 3), this guide provides a comprehensive overview of essential Git commands. It is designed for developers who want to master version control, from basic snapshots to advanced branching and collaboration techniques.*

---

## 1. Getting Started with Git

### 1.1 Installation and Configuration

Before you can start using Git, you need to install it and set up your user identity. This identity is attached to every commit you make, creating a reliable history of contributions.

- **Install Git**: Download from [git-scm.com](https://git-scm.com) for Windows, use `brew install git` on macOS, or `sudo apt install git` on Ubuntu. Verify with `git --version`. 
- **Set your identity**:
    ```bash
    git config --global user.name "Your Name"
    git config --global user.email "your.email@example.com"
    ```
- **Set default editor**:
    ```bash
    git config --global core.editor "code --wait" # Example for Visual Studio Code
    ```

### 1.2 Initializing a Repository

To start version-controlling a project, you need to create a Git repository. This creates a `.git` directory in your project folder, which stores all version history.

```bash
git init
```
This command creates a new Git repository in the current directory. All version control data for your project will now be stored within this hidden `.git` folder. 

### 1.3 Cloning an Existing Repository

To get a copy of an existing project (like one hosted on GitHub), you use `git clone`. This not only downloads the files but also the entire version history and automatically sets up a connection to the original (remote) repository.

```bash
git clone https://github.com/username/repository.git
```
This creates a local copy of the remote repository, complete with all its branches and history. 

---

## 2. Basic Workflow: The Three States

Understanding the three main states of a file in Git is crucial:
1.  **Working Directory**: The files on your system that you are currently working on.
2.  **Staging Area (The Index)**: A file that stores information about what will go into your next commit. You can think of it as a preview or a "build" of your next commit.
3.  **Local Repository (`.git` directory)**: The place where committed data is stored permanently.

A file can be in one of two main statuses: **tracked** (it is in the repository and Git knows about it) or **untracked** (it is a new file that Git hasn't seen before). 

### 2.1 Checking Status

The `git status` command is your primary tool for determining the state of your working directory and staging area. You'll run this constantly to see what's changed, what's staged, and what's untracked. 

```bash
git status
```

### 2.2 Staging Changes

Before you can commit a change, you must stage it. This tells Git which modifications you want to include in your next snapshot. You can stage files individually or all at once.

```bash
git add <filename>
```
Adds a specific file to the staging area. 

```bash
git add .
```
Adds all modified and new files in the current directory and its subdirectories to the staging area. 

### 2.3 Viewing Changes

Before staging, you can review exactly what modifications you've made to your tracked files since your last commit. `git diff` shows the changes in your working directory that are not yet staged. 

```bash
git diff
```
This is an essential command for reviewing your work before creating a commit. 

### 2.4 Committing Changes

Once you have staged your changes, you can save them as a permanent snapshot of your project. A commit is a record of the state of the repository at a specific point in time.

```bash
git commit -m "A descriptive message of the changes"
```
This takes the files you have staged and stores them in the local repository, creating a unique identifier (hash) for the commit. A good commit message is essential for project history. 

### 2.5 Amending the Last Commit

If you've made a commit and then realize you forgot to add a file or you want to change the commit message, you can amend it. This creates a new commit that replaces the previous one. 

```bash
git commit --amend -m "Updated commit message"
```
This is very useful for fixing small mistakes before pushing your code to a remote repository. 

### 2.6 Viewing History

To see the project's history, you can use `git log`. It shows a list of all commits, starting with the most recent, along with their hashes, authors, dates, and messages.

```bash
git log
```
For a more concise view, you can use:
```bash
git log --oneline
```
This shows each commit on a single line, making it easier to scan the history. 

### 2.7 Undoing Changes

Git provides several ways to undo changes, depending on where they are in your workflow. 

- **Unstage a file**: If you've staged a file but want to remove it from the staging area (while keeping your modifications).
    ```bash
    git reset <filename>
    ```
- **Discard a file's changes**: If you want to completely discard changes in your working directory and revert to the last committed version.
    ```bash
    git checkout -- <filename>
    ```
    **Warning:** This action is permanent and cannot be undone.
- **Revert a commit**: Creates a new commit that undoes the changes of a previous commit. This is a safe way to "undo" a commit that has already been pushed to a shared repository.
    ```bash
    git revert <commit-hash>
    ```
- **Reset to a commit**: Moves the `HEAD` pointer and the staging area to a specified commit. This is more powerful and dangerous, especially with `--hard`, as it discards all changes after that commit.
    ```bash
    git reset --hard <commit-hash>
    ```
    **Use this with extreme caution.** It is not suitable for commits that have been pushed to a shared repository. 

---

## 3. Branching: The Killer Feature

Branching is one of Git's most powerful features. It allows you to diverge from the main line of development (e.g., `main` or `master`) and work independently without affecting the primary codebase. This is fundamental for feature development, bug fixing, and experimentation. 

A branch in Git is simply a lightweight movable pointer to a commit. The default branch is usually named `main` or `master`. 

### 3.1 Managing Branches

- **List branches**: Shows all your local branches. The current branch is marked with a `*`.
    ```bash
    git branch
    ```
- **Create a branch**: This creates a new pointer to the commit you are currently on. It does not switch to the new branch.
    ```bash
    git branch <new-branch-name>
    ```
- **Create and switch**: This combines branch creation and switching.
    ```bash
    git checkout -b <new-branch-name>
    ```
- **Switch branches**: Moves your `HEAD` pointer to the specified branch.
    ```bash
    git checkout <branch-name>
    ```
- **Delete a branch**: Deletes the branch. If it contains unmerged work, Git will prevent you from deleting it.
    ```bash
    git branch -d <branch-name>
    ```
- **Force delete a branch**: Deletes the branch even if it contains unmerged work.
    ```bash
    git branch -D <branch-name>
    ```

### 3.2 Merging Branches

Merging is the process of integrating changes from one branch into another. For example, you might merge a `feature-branch` back into the `main` branch.

```bash
git merge <branch-name>
```
This command takes the changes from `<branch-name>` and integrates them into the branch you are currently on. 

### 3.3 Checking Branch Status

Git provides helpful commands to see the relationship between your branches. 

- **Show merged branches**: Lists all branches that have already been merged into the current branch.
    ```bash
    git branch --merged
    ```
- **Show unmerged branches**: Lists all branches that contain work that has not yet been merged into the current branch.
    ```bash
    git branch --no-merged
    ```

---

## 4. Collaborating with Remote Repositories

Working with others involves syncing your local repository with a remote one, often hosted on platforms like GitHub, GitLab, or Bitbucket. 

### 4.1 Managing Remotes

- **Add a remote**: Links your local repository to a remote repository.
    ```bash
    git remote add origin <remote-url>
    ```
    `origin` is the conventional name for the default remote. 
- **List remotes**: Shows the names of your configured remote repositories.
    ```bash
    git remote -v
    ```

### 4.2 Syncing with Remote

- **Push**: Uploads your local commits to the remote repository.
    ```bash
    git push origin <branch-name>
    ```
    This makes your commits available to other collaborators. 
- **Pull**: Downloads changes from the remote repository and immediately merges them into your current local branch.
    ```bash
    git pull origin <branch-name>
    ```
    This is a combination of `git fetch` and `git merge`. 

---

## 5. Advanced Commands and Techniques

### 5.1 Stashing

Sometimes you need to switch branches but aren't ready to commit your current work. `git stash` temporarily shelves (or stashes) your uncommitted changes so you can work on something else.

```bash
git stash
```
You can later reapply the stashed changes:
```bash
git stash pop
```
This is a great tool for context switching. 

### 5.2 Interactive Staging (`add -p`)

For more granular control over your commits, you can stage changes in parts. `git add -p` allows you to review each change in your files and decide whether to stage it or not. This is a powerful way to create clean, focused commits.

```bash
git add -p
```
This command will walk you through each hunk of changes in your files, asking if you want to stage it. 

### 5.3 Squashing Commits

Before merging a feature branch into `main`, it's often a good idea to "squash" or combine several related commits into a single, clean commit. This creates a clearer project history.

```bash
git rebase -i HEAD~<number-of-commits>
```
In the interactive editor that opens, you can change `pick` to `squash` (or `s`) for the commits you want to combine into the one before them. 

### 5.4 Recovering Lost Work (`reflog`)

Git keeps a record of when the tips of branches and other references were updated in the repository. This log is called the `reflog`. It's a powerful safety net for recovering commits that may have been lost due to a `reset` or a messy rebase. 

```bash
git reflog
```
This shows a history of all your `HEAD` movements. You can then use `git checkout` or `git reset` to recover a specific state.

### 5.5 Git Hooks

Git hooks are scripts that Git runs before or after events like `commit`, `push`, or `receive`. They are a powerful way to enforce policies, run automated tests, or perform formatting checks. 

- **Client-side hooks**: Run on your local machine (e.g., `pre-commit` for linting, `commit-msg` for message validation).
- **Server-side hooks**: Run on the server (e.g., `pre-receive` for rejecting pushes that don't meet criteria).

For example, a `pre-commit` hook might run a linter to ensure code quality before a commit is allowed. 
