# Git Beginner Lab: Step-by-Step Workflow Guide by Alan Soto

This document outlines the fundamental workflow for initializing, managing, and collaborating on a Git repository, from initial local setup to pushing changes to a remote GitHub repository.

---

## Section 1: Environment Setup & Global Configuration
In this initial phase, we verify the Git installation, check our current directory, and configure our global user identity and preferred text editor.

| Step | Action / Description | Commands | Screenshot |
| :--- | :--- | :--- | :--- |
| **1.1** | Check the installed Git version and inspect the current working directory. | `git --version`<br>`pwd`<br>`ls` | <img width="1220" height="340" alt="image" src="https://github.com/user-attachments/assets/bf617d32-478d-4152-a340-7f61e78c7515" /> |
| **1.2** | Configure global username, email, default editor (VS Code), and line-ending handling. | `git config --global user.name "Alan Soto"`<br>`git config --global user.email example@hotmail.com`<br>`git config --global core.editor "code --wait"`<br>`git config --global core.autocrlf true` | <img width="1046" height="345" alt="image" src="https://github.com/user-attachments/assets/1ffd8053-ca9f-4d9d-9c6b-22c0efd7d70a" /> |
| **1.3** | Review the global configuration file to verify all settings were saved properly. | `git config --global -e` | <img width="1340" height="846" alt="image" src="https://github.com/user-attachments/assets/247ad76f-902a-4b51-9fe6-44bc3f57f960" /> |

---

## Section 2: Repository Initialization & Inspection
Here, we create a new project folder, initialize a local Git repository, and explore the hidden `.git` directory where Git stores its metadata.

| Step | Action / Description | Commands | Screenshot |
| :--- | :--- | :--- | :--- |
| **2.1** | Navigate to the `Documents` folder, create the `data-engineering` project directory, and move into it. | `cd Documents/`<br>`mkdir data-engineering/`<br>`cd data-engineering/` | <img width="1042" height="187" alt="image" src="https://github.com/user-attachments/assets/ebf048ac-c99c-426e-be18-67a3d06e66ef" /> |
| **2.2** | Initialize an empty Git repository and list visible and hidden files (`-a`) to verify the `.git` folder creation. | `git init`<br>`ls`<br>`ls -a` | <img width="1116" height="207" alt="image" src="https://github.com/user-attachments/assets/d4f411c2-34da-4eb4-a00b-089bcd77d54e" /> |
| **2.3** | Inspect the internal contents of the `.git` directory, return to the project root, and launch VS Code. | `cd .git`<br>`ls -a`<br>`cd ..`<br>`code .` | <img width="1124" height="450" alt="image" src="https://github.com/user-attachments/assets/38755c25-1292-4545-9601-bcbff8e46687" /> <img width="1432" height="794" alt="Captura de pantalla 2026-11-22 190957" src="https://github.com/user-attachments/assets/4c7a77bb-892d-46c8-a3f1-ed1de5823d07" /> |

---

## Section 3: Staging & Committing Files (The Basic Cycle)
In this section, we practice the core Git workflow: creating files, checking repository status, adding changes to the staging area, and saving snapshots (commits).

| Step | Action / Description | Commands | Screenshot |
| :--- | :--- | :--- | :--- |
| **3.1** | Create a `README.md` file in VS Code, check the repository status, stage the file, and create the first commit. | *(Create `README.md` in VS Code)*<br>`git status`<br>`git add README.md`<br>`git status`<br>`git commit -m "Primer commit, creamos README"` | <img width="726" height="342" alt="Captura de pantalla 2026-11-22 191103" src="https://github.com/user-attachments/assets/a068de64-3a47-4fe8-9095-f77b5721215d" />  <img width="1273" height="944" alt="image" src="https://github.com/user-attachments/assets/45ef757b-5b09-42bb-9e38-4f8294cf4425" /> |
| **3.2** | List files, create a second file (`archivo2.txt`), stage it, and commit it to the repository history. | `ls`<br>*(Create `archivo2.txt` in VS Code)*<br>`git status`<br>`git add archivo2.txt`<br>`git status`<br>`git commit -m "Nuevo archivo"` | <img width="898" height="367" alt="Captura de pantalla 2026-11-22 191306" src="https://github.com/user-attachments/assets/bff23b8a-7058-4ae7-9dcb-2fb8b48ee882" /> <img width="1261" height="994" alt="image" src="https://github.com/user-attachments/assets/4d4c8eee-4a95-4d05-bcde-5fa77d3929c1" /> |

---

## Section 4: Ignoring Sensitive Files (`.gitignore`)
When working with credentials or environment variables, we must prevent Git from tracking sensitive files.

| Step | Action / Description | Commands | Screenshot |
| :--- | :--- | :--- | :--- |
| **4.1** | Create a test `.env` file containing sensitive data in VS Code and check `git status` (it will appear as untracked). | *(Create `.env` in VS Code)*<br>`git status` | <img width="824" height="257" alt="Captura de pantalla 2026-11-22 195215" src="https://github.com/user-attachments/assets/7e0673a1-ac81-4722-bb9e-7ff9e478f1fd" /> <img width="1226" height="261" alt="image" src="https://github.com/user-attachments/assets/d0d687ca-2f79-4c3b-b9e9-f0e6ba4395db" /> |
| **4.2** | Create a `.gitignore` file, add `.env` inside it, and verify that Git now ignores the `.env` file. | *(Create `.gitignore` and add `.env` inside)*<br>`git status` | <img width="819" height="281" alt="Captura de pantalla 2026-11-22 195301" src="https://github.com/user-attachments/assets/fae75efe-448a-47f9-b265-add0a8a71e93" /> <img width="1245" height="272" alt="Captura de pantalla 2026-11-22 195314" src="https://github.com/user-attachments/assets/e0705957-49fb-4d66-a8b0-2eb89f363438" /> |
| **4.3** | Stage and commit the `.gitignore` file so the ignore rules are saved in the repository. | `git add .gitignore`<br>`git commit -m ".gitignore para ignorar los cambios en .env"`<br>`git status` | <img width="1233" height="904" alt="image" src="https://github.com/user-attachments/assets/fc4d4f7e-c7d4-4a68-8c7d-6db65a9ebf65" /> |

---

## Section 5: File Management & History Inspection
In this block, we rename tracked files using Git commands, inspect differences between changes, and review the commit history.

| Step | Action / Description | Commands | Screenshot |
| :--- | :--- | :--- | :--- |
| **5.1** | Rename `archivo2.txt` to `LEARNING_LOG.md`, check the short status (`-s`), and commit the change. | `git mv archivo2.txt LEARNING_LOG.md`<br>`git status -s`<br>`git commit -m "Se da el nombre y tipo del archivo correcto"` | <img width="1046" height="609" alt="image" src="https://github.com/user-attachments/assets/a0d05261-2c4a-4076-ad33-b39f1c148faf" /> |
| **5.2** | Inspect unstaged/staged changes and view the commit history in full and compact (`--oneline`) formats. | `git diff`<br>`git diff --staged`<br>`git log`<br>`git log --oneline` | <img width="1112" height="981" alt="image" src="https://github.com/user-attachments/assets/50ef7534-3258-48d3-9422-d9fc48c6f878" /> |

---

## Section 6: Undoing Changes & File Recovery
Git allows you to safely discard unwanted modifications or recover accidentally deleted files from the staging area or working directory.

| Step | Action / Description | Commands | Screenshot |
| :--- | :--- | :--- | :--- |
| **6.1** | Modify `LEARNING_LOG.md`, check status, and discard the local changes to restore it to its last committed state. | *(Edit `LEARNING_LOG.md`)*<br>`git status`<br>`git restore LEARNING_LOG.md`<br>`git status` | <img width="897" height="272" alt="Captura de pantalla 2026-11-22 200242" src="https://github.com/user-attachments/assets/6670863f-2e4d-4a39-adab-9caefdc8e954" /> <img width="1170" height="518" alt="image" src="https://github.com/user-attachments/assets/669f6f16-492a-4df1-9169-e2036720d3fc" /> |
| **6.2** | Delete `LEARNING_LOG.md` using `git rm`, unstage the deletion with `--staged`, and restore the file to the working directory. | `git rm LEARNING_LOG.md`<br>`ls`<br>`git status`<br>`git restore --staged LEARNING_LOG.md`<br>`git status`<br>`git restore LEARNING_LOG.md` | <img width="1279" height="1330" alt="image" src="https://github.com/user-attachments/assets/ad206300-6d52-4a2f-b98a-3534b02578d6" /> |

---

## Section 7: Branching & Merging
Branches allow you to develop features or make edits in an isolated environment without affecting the `main` branch until you are ready to merge.

| Step | Action / Description | Commands | Screenshot |
| :--- | :--- | :--- | :--- |
| **7.1** | List existing branches, create a new branch named `ramab`, and switch to it immediately. | `git branch`<br>`git checkout -b ramab`<br>`git branch` | <img width="1003" height="375" alt="image" src="https://github.com/user-attachments/assets/e38f9436-1de1-44d1-8308-3b41ff026f46" /> |
| **7.2** | Edit `LEARNING_LOG.md` inside `ramab`, stage, commit the changes, and display the file content. | *(Edit `LEARNING_LOG.md`)*<br>`git status`<br>`git add LEARNING_LOG.md`<br>`git commit -m "Cambio desde la ramab"`<br>`cat LEARNING_LOG.md` | <img width="1271" height="746" alt="image" src="https://github.com/user-attachments/assets/dc98343b-2a41-43b6-bec9-b875268d34c1" /> |
| **7.3** | Switch back to the `main` branch, verify the changes are not there yet, and merge `ramab` into `main`. | `git checkout main`<br>`cat LEARNING_LOG.md`<br>`git merge ramab` | <img width="1274" height="518" alt="image" src="https://github.com/user-attachments/assets/265c8459-cad5-4480-8675-4dafdfbcfe46" /> |

---

## Section 8: Remote Repository & GitHub Synchronization
Finally, we connect our local repository to a remote GitHub repository and upload our commit history.

| Step | Action / Description | Commands | Screenshot |
| :--- | :--- | :--- | :--- |
| **8.1** | Link the local repository to the remote GitHub URL using the alias `origin`. | `git remote add origin https://github.com/arrebolcorp/data-engineering-w36.git` | <img width="1250" height="1255" alt="Captura de pantalla 2026-11-22 201644" src="https://github.com/user-attachments/assets/d1f6fd9e-2805-4a29-a920-a34d965f8d3f" /> <img width="1284" height="162" alt="image" src="https://github.com/user-attachments/assets/32ebdaac-cdd8-4b69-8993-4a3400d5e5be" /> |
| **8.2** | Push the local `main` branch to GitHub (`-u` sets upstream tracking) and verify the files on the GitHub website. | `git push -u origin main`<br>*(Verify files on GitHub repository page)* | <img width="1097" height="402" alt="image" src="https://github.com/user-attachments/assets/17bf4d0b-d5de-48d5-bca1-f5a698286bea" /> <img width="1227" height="1037" alt="Captura de pantalla 2026-11-22 201736" src="https://github.com/user-attachments/assets/72a4a41c-92ac-411a-ba77-47ede25745c1" /> |
