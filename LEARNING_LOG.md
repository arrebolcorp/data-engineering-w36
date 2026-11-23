# Git Beginner Lab: Step-by-Step Workflow Guide

This document outlines the fundamental workflow for initializing, managing, and collaborating on a Git repository, from initial local setup to pushing changes to a remote GitHub repository.

---

## Section 1: Environment Setup & Global Configuration
In this initial phase, we verify the Git installation, check our current directory, and configure our global user identity and preferred text editor.

| Step | Action / Description | Commands | Screenshot |
| :--- | :--- | :--- | :--- |
| **1.1** | Check the installed Git version and inspect the current working directory. | `git --version`<br>`pwd`<br>`ls` | *[Insert Screenshot 1.1 here]* |
| **1.2** | Configure global username, email, default editor (VS Code), and line-ending handling. | `git config --global user.name "Alan Soto"`<br>`git config --global user.email jahirmiranda.12@hotmail.com`<br>`git config --global core.editor "code --wait"`<br>`git config --global core.autocrlf true` | *[Insert Screenshot 1.2 here]* |
| **1.3** | Review the global configuration file to verify all settings were saved properly. | `git config --global -e` | *[Insert Screenshot 1.3 here]* |

---

## Section 2: Repository Initialization & Inspection
Here, we create a new project folder, initialize a local Git repository, and explore the hidden `.git` directory where Git stores its metadata.

| Step | Action / Description | Commands | Screenshot |
| :--- | :--- | :--- | :--- |
| **2.1** | Navigate to the `Documents` folder, create the `data-engineering` project directory, and move into it. | `cd Documents/`<br>`mkdir data-engineering/`<br>`cd data-engineering/` | *[Insert Screenshot 2.1 here]* |
| **2.2** | Initialize an empty Git repository and list visible and hidden files (`-a`) to verify the `.git` folder creation. | `git init`<br>`ls`<br>`ls -a` | *[Insert Screenshot 2.2 here]* |
| **2.3** | Inspect the internal contents of the `.git` directory, return to the project root, and launch VS Code. | `cd .git`<br>`ls -a`<br>`cd ..`<br>`code .` | *[Insert Screenshot 2.3 here]* |

---

## Section 3: Staging & Committing Files (The Basic Cycle)
In this section, we practice the core Git workflow: creating files, checking repository status, adding changes to the staging area, and saving snapshots (commits).

| Step | Action / Description | Commands | Screenshot |
| :--- | :--- | :--- | :--- |
| **3.1** | Create a `README.md` file in VS Code, check the repository status, stage the file, and create the first commit. | *(Create `README.md` in VS Code)*<br>`git status`<br>`git add README.md`<br>`git status`<br>`git commit -m "Primer commit, creamos README"` | *[Insert Screenshot 3.1 here]* |
| **3.2** | List files, create a second file (`archivo2.txt`), stage it, and commit it to the repository history. | `ls`<br>*(Create `archivo2.txt` in VS Code)*<br>`git status`<br>`git add archivo2.txt`<br>`git status`<br>`git commit -m "Nuevo archivo"` | *[Insert Screenshot 3.2 here]* |

---

## Section 4: Ignoring Sensitive Files (`.gitignore`)
When working with credentials or environment variables, we must prevent Git from tracking sensitive files.

| Step | Action / Description | Commands | Screenshot |
| :--- | :--- | :--- | :--- |
| **4.1** | Create a test `.env` file containing sensitive data in VS Code and check `git status` (it will appear as untracked). | *(Create `.env` in VS Code)*<br>`git status` | *[Insert Screenshot 4.1 here]* |
| **4.2** | Create a `.gitignore` file, add `.env` inside it, and verify that Git now ignores the `.env` file. | *(Create `.gitignore` and add `.env` inside)*<br>`git status` | *[Insert Screenshot 4.2 here]* |
| **4.3** | Stage and commit the `.gitignore` file so the ignore rules are saved in the repository. | `git add .gitignore`<br>`git commit -m ".gitignore para ignorar los cambios en .env"`<br>`git status` | *[Insert Screenshot 4.3 here]* |

---

## Section 5: File Management & History Inspection
In this block, we rename tracked files using Git commands, inspect differences between changes, and review the commit history.

| Step | Action / Description | Commands | Screenshot |
| :--- | :--- | :--- | :--- |
| **5.1** | Rename `archivo2.txt` to `LEARNING_LOG.md`, check the short status (`-s`), and commit the change. | `git mv archivo2.txt LEARNING_LOG.md`<br>`git status -s`<br>`git commit -m "Se da el nombre y tipo del archivo correcto"` | *[Insert Screenshot 5.1 here]* |
| **5.2** | Inspect unstaged/staged changes and view the commit history in full and compact (`--oneline`) formats. | `git diff`<br>`git diff --staged`<br>`git log`<br>`git log --oneline` | *[Insert Screenshot 5.2 here]* |

---

## Section 6: Undoing Changes & File Recovery
Git allows you to safely discard unwanted modifications or recover accidentally deleted files from the staging area or working directory.

| Step | Action / Description | Commands | Screenshot |
| :--- | :--- | :--- | :--- |
| **6.1** | Modify `LEARNING_LOG.md`, check status, and discard the local changes to restore it to its last committed state. | *(Edit `LEARNING_LOG.md`)*<br>`git status`<br>`git restore LEARNING_LOG.md`<br>`git status` | *[Insert Screenshot 6.1 here]* |
| **6.2** | Delete `LEARNING_LOG.md` using `git rm`, unstage the deletion with `--staged`, and restore the file to the working directory. | `git rm LEARNING_LOG.md`<br>`ls`<br>`git status`<br>`git restore --staged LEARNING_LOG.md`<br>`git status`<br>`git restore LEARNING_LOG.md` | *[Insert Screenshot 6.2 here]* |

---

## Section 7: Branching & Merging
Branches allow you to develop features or make edits in an isolated environment without affecting the `main` branch until you are ready to merge.

| Step | Action / Description | Commands | Screenshot |
| :--- | :--- | :--- | :--- |
| **7.1** | List existing branches, create a new branch named `ramab`, and switch to it immediately. | `git branch`<br>`git checkout -b ramab`<br>`git branch` | *[Insert Screenshot 7.1 here]* |
| **7.2** | Edit `LEARNING_LOG.md` inside `ramab`, stage, commit the changes, and display the file content. | *(Edit `LEARNING_LOG.md`)*<br>`git status`<br>`git add LEARNING_LOG.md`<br>`git commit -m "Cambio desde la ramab"`<br>`cat LEARNING_LOG.md` | *[Insert Screenshot 7.2 here]* |
| **7.3** | Switch back to the `main` branch, verify the changes are not there yet, and merge `ramab` into `main`. | `git checkout main`<br>`cat LEARNING_LOG.md`<br>`git merge ramab` | *[Insert Screenshot 7.3 here]* |

---

## Section 8: Remote Repository & GitHub Synchronization
Finally, we connect our local repository to a remote GitHub repository and upload our commit history.

| Step | Action / Description | Commands | Screenshot |
| :--- | :--- | :--- | :--- |
| **8.1** | Link the local repository to the remote GitHub URL using the alias `origin`. | `git remote add origin https://github.com/arrebolcorp/data-engineering-w36.git` | *[Insert Screenshot 8.1 here]* |
| **8.2** | Push the local `main` branch to GitHub (`-u` sets upstream tracking) and verify the files on the GitHub website. | `git push -u origin main`<br>*(Verify files on GitHub repository page)* | *[Insert Screenshot 8.2 here]* |