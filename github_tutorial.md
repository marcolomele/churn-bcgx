# GitHub Tutorial for Team Collaboration

This guide explains how to use our GitHub repository for collaboration. 

## Setting Up (One-time Process)

### 1. Install Git

- **Windows**: Download and install from [git-scm.com](https://git-scm.com/download/win)
- **Mac**: Install with Homebrew using `brew install git` or download from [git-scm.com](https://git-scm.com/download/mac)
- **Linux**: Use your package manager, e.g., `sudo apt-get install git` (Ubuntu/Debian)

### 2. Configure Git (First-time only)

Open your terminal or command prompt and set your identity:

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

### 3. Clone the Repository

This downloads a copy of the repository to your computer:

```bash
git clone https://github.com/username/repository-name.git
```

Replace `username/repository-name` with our actual repository URL.

This creates a new folder with the repository name. Navigate into it:

```bash
cd repository-name
```
## Repo Structure

We'll keep things simple by working on the main branch and using folders to organize our work. We're using folders to organize different parts of the project. Work only in your assigned folders to avoid conflicts. When a file is in its final version, move it to the main branch. The idea is to not edit directly in the main folder. 

Folders:
- `/main` - Contains final versions of files
- `/giova` - Giova's working folder
- `/ilia` - Ilia's working folder
- `/javi` - Javi's working folder
- `/marco` - Marco's working folder
- `/santi` - Santi's working folder

Other files:
- .gitinore – tells GitHub which files to ignore and not upload. To ignore a file in you folder, in a new line write `{your_folder}/{file_name.file_type}`
- LICENSE – what licence we give others to use our code, currently set to open source

### Working in Your Folder and Moving to Main

1. Always edit files in your own named folder (e.g., `/javi`, `/santi`, etc.). Organise your folder as you prefer, making sure to keep track of what is the final version of things. 
2. When a file is in its final version and ready to be moved to main:
   
   ```bash
   # First, ensure you have the latest changes
   git pull --rebase
   
   # Copy your file to the main folder
   cp yourfolder/yourfile.ext main/yourfile.ext
   
   # Add both your working file and the main copy
   git add yourfolder/yourfile.ext main/yourfile.ext
   
   # Commit with clear message mentioning the move to main
   git commit -m "Finalized feature X and moved to main"
   
   # Push your changes
   git push
   ```

Remember that the `/main` folder is for final versions only. All development work should happen in your personal folder.

## Daily Workflow
Everything that is described below can also be done easily with buttons in VS Code. Tutorial videos: 
- [git in 100 seconds](https://www.youtube.com/watch?v=hwP7WQkmECE) 
- [general overview](https://www.youtube.com/watch?v=i_23KUAEtUM)
- [longer tutorial](https://www.youtube.com/watch?v=z5jZ9lrSpqk&t=646s)
- [why we dull pull rebase](https://www.youtube.com/watch?v=f1wnYdLEpgI)

### 1. Getting the Latest Changes

Before you start working, always get the latest changes from the repository:

```bash
git pull --rebase
```

Using `--rebase` helps avoid merge conflicts by placing your changes on top of the latest changes from others.

### 2. Creating Your Work

We're organizing work by folders instead of branches. If more people are working on the same file, copy and paste the file in your own folder.  

### 3. Making Changes

After editing or adding files:

1. Check which files you've changed:

```bash
git status
```

2. Add your changes to the staging area:

```bash
git add .
```

This adds all changed files. To add specific files only:

```bash
git add folder-name/file-name
```

3. Commit your changes with a descriptive message:

```bash
git commit -m "Brief description of what you changed"
```

### 4. Uploading Your Changes

Push your committed changes to GitHub:

```bash
git pull --rebase
git push
```

We do another `git pull --rebase` right before pushing to make sure we have the latest changes.

IMPORTANT: Always pull before you start working and before you push!

## Best Practices for Collaboration

### Naming Conventions
- Use clear, descriptive file names (e.g., `user-authentication.js` instead of `auth.js`)
- Avoid spaces in file names; use hyphens instead (e.g., `meeting-notes.md` not `meeting notes.md`)
- Use consistent lowercase naming for files to avoid case-sensitivity issues

### Commit Messages
- Write descriptive commit messages that explain what and why (not how)
- Start with a verb in present tense (e.g., "Add login functionality" not "Added login functionality")
- Keep messages under 50 characters when possible
- For complex changes, add details after a blank line in the commit message

### Communication
- Comment your code appropriately
- Update the team on significant changes via your agreed communication channel
- When stuck, ask for help early rather than making major changes out of frustration

### Working Habits
- Commit small, logical chunks of work rather than large changes
- Pull changes at the beginning of your work session
- Always verify changes worked before pushing
- Take extra care when moving files to the `/main` folder

## Common Scenarios & Troubleshooting

### Discarding Changes (Before Committing)

If you made changes you don't want to keep:

```bash
git restore filename
```

Or to discard all changes:

```bash
git restore .
```

### If you get a conflict message:

1. Open the conflicted file(s)
2. Look for sections marked with `<<<<<<`, `======`, and `>>>>>>>`
3. Edit these sections to resolve the conflict
4. Save the file(s)
5. Add and commit the resolved files:

```bash
git add .
git commit -m "Resolve conflicts"
git push
```

### If you added a file to track and want to undo git add
```bash
git reset file_name.file_type
```

### If you forgot to pull before working:

```bash
git stash
git pull --rebase
git stash pop
```

This temporarily stores your changes, gets the latest updates, then reapplies your changes.

### If you committed but haven't pushed and want to change your commit message:

```bash
git commit --amend -m "New improved commit message"
```

### If you need to see who made specific changes to a file:

```bash
git blame filename
```

This shows who last modified each line of the file.

### If you need to undo your most recent commit but keep the changes:

```bash
git reset --soft HEAD~1
```

### If you need to see what changes you're about to commit:

```bash
git diff --staged
```

### If you committed to the wrong folder:

```bash
# Undo the commit but keep the changes
git reset --soft HEAD~1

# Move the files to the correct location
mv wrongfolder/file.ext correctfolder/file.ext

# Add and commit again
git add correctfolder/file.ext
git commit -m "Add file to correct folder"
```