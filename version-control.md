## To push selective files and folders from [your local directory] (C:\GoogleDrive_MyDrive\scripts\CDISC-ADaM-dataset-creation) to a GitHub repository, follow these steps

## Initialize a Git Repository (if not already done)
Open a terminal (or Git Bash if you're on Windows).

Navigate to the directory:
```bash
cd C:/GoogleDrive_MyDrive/scripts/CDISC-ADaM-dataset-creation
```

Initialize the Git repository:
```bash
git init
```
This creates C:/GoogleDrive_MyDrive/scripts/CDISC-ADaM-dataset-creation/.git

## Add a Remote Repository
Go to your GitHub account and create a new repository 

Copy the repository's URL https://github.com/luenhchang/CDISC-ADaM-dataset-creation.git

Add the remote to your local Git repository:
```
bash
git remote add origin https://github.com/luenhchang/CDISC-ADaM-dataset-creation.git
```

## Selectively Stage Files and Folders
Stage (select) files and folders:
```bash
git add creating-ADSL-using-admiral-package.md creating-ADSL-using-admiral-package.qmd
```

Verify the staged files. This will list new files to commit and untracked files (files, folders that won't be committed)
```bash
git status
```

## Commit the Changes
Commit the staged files with a meaningful message
```bash
git commit -m "Add files to remote"
```

## Push to GitHub
Push the committed changes to the main branch of your GitHub repository:
```bash
git push origin main
```

## Create a .gitignore file
If you want to use git add . to stage all changes in the directory but still exclude certain files and folders from being committed to the repository, creating a .gitignore file is the best approach

Navigate to your project directory:
```bash
cd "C:/GoogleDrive_MyDrive/scripts/CDISC-ADaM-dataset-creation"
```

Create a .gitignore file:
```bash
touch .gitignore
```
Or, create it using a text editor (e.g., Notepad, VS Code).

## Define Files/Folders to Ignore
Add the files and directories you want to exclude to the .gitignore file. 
```gitignore
# Ignore specific files
# Ignore specific folders
references/

# Ignore log files
*.log

# Ignore temporary files
*.tmp
*.bak
```

## Stage and Commit the .gitignore File
Once the .gitignore file is set up, commit it to the repository so that Git knows to respect it
```bash
git add .gitignore
git commit -m "Add .gitignore file to exclude unwanted files and folders"
git push origin main
```

## Using git add . Safely for subsequent changes
After setting up the .gitignore file:

1. Use git add . to stage all files except those listed in .gitignore:\
```bash
git add .
```

2. Verify the staged files with:
```bash
git status
```

3.Commit and push changes:
```bash
git commit -m "Commit all changes"
git push origin main
```

## Create README.md
### Option 1: Create README.md Locally
Advantages:
* Offline Editing: You can write and format the README.md without needing an internet connection.
* Familiar Tools: Use your favorite text editor (e.g., VS Code, Sublime Text, or Notepad++) to write the file.
* Version Control: You can easily track changes to the README.md file in your local repository and commit those changes as part of your version history.

Steps:
Create the file locally:
```bash
touch README.md
```

Edit the file using your preferred editor.

Add, commit, and push the file to GitHub:
```bash
git add README.md
git commit -m "Add README.md"
git push origin main
```

## Render PDF
The error message indicates that Quarto cannot detect a TeX installation on your system, which is necessary for rendering PDF documents. 

Install Quarto CLI in Windows:
Location of quarto.exe is at
C:\Users\luenh\AppData\Local\Programs\Quarto\bin\quarto.exe

Add the folder path to Path Variable

```bash
quarto --Version
1.6.39
```

Install TinyTeX via Quarto:
```bash
quarto install tinytex
```

Install TinyTeX in RStudio
If you haven't installed TinyTeX in RStudio, you can do so directly from the R console. Run the following:

```r
install.packages("tinytex")
# install the latest version of xfun
install.packages("xfun")
packageVersion("xfun")
#[1] ‘0.49’
tinytex::install_tinytex()
```
render pdf in RStudio

## Stop tracking a specific file
The reason CDISC-ADaM-dataset-creation.Rproj is still appearing in your Git repository despite being listed in your .gitignore might be because it was added to the repository before you added it to the .gitignore file. Git doesn't automatically remove files from the repository just because they are added to .gitignore after they've already been tracked.

To fix this, follow these steps:

1. Check if .Rproj is tracked by Git
You can check if the .Rproj file is already tracked by Git with the following command:

```bash
git ls-files
```
This will list all files currently being tracked by Git.

If you see CDISC-ADaM-dataset-creation.Rproj in the output, it means that the file is being tracked.

2. Remove the .Rproj file from Git tracking
To stop tracking the .Rproj file, you need to remove it from Git's index, without deleting it from your local file system:

```bash
git rm --cached CDISC-ADaM-dataset-creation.Rproj
```
3. Commit the change
After removing it from the index, commit the change:

```bash
git commit -m "Stop tracking .Rproj file"
```
4. Push the changes
Finally, push the changes to your remote repository:

```bash
git push origin main
```
5. Verify .gitignore
Make sure that the .gitignore file contains the correct pattern to ignore .Rproj files. You should have something like this in your .gitignore:

*.Rproj

## 2025-01-03
```bash
cd C:/GoogleDrive_MyDrive/scripts/CDISC-ADaM-dataset-creation
```
 
