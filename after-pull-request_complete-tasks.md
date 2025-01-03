# [pharmaverse/admiral] 2578 unit test (PR #2594)

Vladyslav Shuliar <notifications@github.com>
3:00 AM (7 hours ago)
to pharmaverse/admiral, Subscribed

Thank you for your Pull Request! We have developed this task checklist from the Development Process Guide to help with the final steps of the process. Completing the below tasks helps to ensure our reviewers can maximize their time on your code as well as making sure the admiral codebase remains robust and consistent.

Please check off each taskbox as an acknowledgment that you completed the task or check off that it is not relevant to your Pull Request. This checklist is part of the Github Action workflows and the Pull Request will not be merged into the main branch until you have checked off each task.

1. Place Closes #<insert_issue_number> into the beginning of your Pull Request Title (Use Edit button in top-right if you need to update)
2. Code is formatted according to the tidyverse style guide. Run styler::style_file() to style R and Rmd files
3. Updated relevant unit tests or have written new unit tests, which should consider realistic data scenarios and edge cases, e.g. empty datasets, errors, boundary cases etc. - See [Unit Test Guide](https://pharmaverse.github.io/admiraldev/articles/unit_test_guidance.html#tests-should-be-robust-to-cover-realistic-data-scenarios)
4. If you removed/replaced any function and/or function parameters, did you fully follow the deprecation guidance?
5. Review the Cheat Sheet. Make any required updates to it by editing the file inst/cheatsheet/admiral_cheatsheet.pptx and re-upload a PDF and a PNG version of it to the same folder. (The PNG version can be created by taking a screenshot of the PDF version.)
6. Update to all relevant roxygen headers and examples, including keywords and families. Refer to the categorization of functions to tag appropriate keyword/family.
7. Run devtools::document() so all .Rd files in the man folder and the NAMESPACE file in the project root are updated appropriately
8. Address any updates needed for vignettes and/or templates
9. Update NEWS.md under the header # admiral (development version) if the changes pertain to a user-facing function (i.e. it has an @export tag) or documentation aimed at users (rather than developers). A Developer Notes section is available in NEWS.md for tracking developer-facing issues.
10. Build admiral site pkgdown::build_site() and check that all affected examples are displayed correctly and that all new functions occur on the "Reference" page.
11. Address or fix all lintr warnings and errors - lintr::lint_package()
12. Run R CMD check locally and address all errors and warnings - devtools::check()
13. Link the issue in the Development Section on the right hand side.
14. Address all merge conflicts and resolve appropriately
15. Pat yourself on the back for a job well done! Much love to your accomplishment!

## Add Closes #<issue_number> to the pull request (PR) Title
old title: "feat: Add my_first_fcn to welcome new users #2593"
New title: "Closes #2593 feat: Add my_first_fcn to welcome new users"  

## Format Code with tidyverse Style Guide
Run styler::style_file() in R for all modified .R and .Rmd files:

```r
install.packages("styler")

#styler::style_file("path/to/your/file.R")
setwd("C:/GoogleDrive_MyDrive/GitHub/admiral-development/admiral")

styler::style_file("R/my_first_fcn.R")
#Styling  1  files:
# R/my_first_fcn.R ℹ 
#────────────────────────────────────────
#Status	Count	Legend 
#✔ 	0	File unchanged.
#ℹ 	1	File changed.
#✖ 	0	Styling threw an error.
#────────────────────────────────────────
#Please review the changes carefully!

styler::style_file("tests/testthat/test-my_first_fcn.R")
#Styling  1  files:
# tests/testthat/test-my_first_fcn.R ℹ 
#────────────────────────────────────────
#Status	Count	Legend 
#✔ 	0	File unchanged.
#ℹ 	1	File changed.
#✖ 	0	Styling threw an error.
#────────────────────────────────────────
#Please review the changes carefully!
```

Stage the files:
```
bash
cd C:/GoogleDrive_MyDrive/GitHub/admiral-development/admiral
git add tests/testthat/test-my_first_fcn.R R/my_first_fcn.R
```

Commit the changes:
```
bash
git commit -m "style: Apply tidyverse style to my_first_fcn.R and its test file"
```

Show the current branch and its tracking status
```
bash
git status
On branch feature/my_first_fcn
Your branch is ahead of 'origin/feature/my_first_fcn' by 1 commit.
  (use "git push" to publish your local commits)
```
  
Push the changes to your branch:
```bash
git push
```
You should not use git push origin main in this case because you're working on a feature branch associated with a Pull Request, not directly on the main branch. Using git push origin main would attempt to push changes to the main branch, which:

* May not be allowed if the repository enforces branch protections (as is typical in collaborative projects).
* Could disrupt the main branch by introducing incomplete or unreviewed changes.

## Fix the Documentation Action

### What is a .Rd file?
A .Rd file is a Roxygen Documentation file used in R programming for documenting functions, datasets, or packages. These files are written in a specific format that combines plain text with markup tags to describe the functionality, arguments, and other details of R functions or data. The .Rd files are stored in the man/ directory of an R package.

The file `man\my_first_fcn.Rd` is the one that will be updated after running devtools::document() in `R/my_first_fcn.R`

### Contents in a .Rd file
Before running devtools::document(), examine the contents in `my_first_fcn.Rd`. Its current contents:

% Generated by roxygen2: do not edit by hand
% Please edit documentation in R/my_first_fcn.R
\name{my_first_fcn}
\alias{my_first_fcn}
\title{My First Function}
\usage{
my_first_fcn()
}
\value{
A string with a welcome message.
}
\description{
This function outputs a welcome message for onboarding purposes.
}

The content of your my_first_fcn.Rd file matches the standard format for an R documentation file generated by roxygen2. Based on this .Rd file:

1. Overview:

\name: Defines the function's name, my_first_fcn.
\alias: Makes the function accessible via the same name in the help system.
\title: Short title for the function.
\usage: Shows how the function is used (my_first_fcn() with no arguments in this case).
\value: Describes the return value of the function, which is a string containing a welcome message.
\description: A brief explanation of what the function does.

2. Generated by roxygen2:

The file header indicates it was generated automatically: % Generated by roxygen2: do not edit by hand.
The line % Please edit documentation in R/my_first_fcn.R suggests that any changes to the documentation should be made in the source file (my_first_fcn.R) using #' comments.

3. Next Steps:

If you modify the documentation in R/my_first_fcn.R (for example, by adding more #' comments), you need to rerun devtools::document() to update the .Rd file.
After running devtools::document(), check that the my_first_fcn.Rd file reflects the latest changes.

### Run devtools::document() so all .Rd files in the man folder and the NAMESPACE file in the project root are updated appropriately

Open `R/my_first_fcn.R` 

Change current working directory to the root of your package directory. This is because `devtools::document()` relies on the directory structure and expects to find files like DESCRIPTION, NAMESPACE, and the R/ folder in the correct locations relative to the working directory.

Make a change in R/my_first_fcn.R
Change the Roxygen2 comment from #' @return A string with a welcome message. to  #' @return A string with a welcome message "Welcome to admiral!"
```r
setwd("C:/GoogleDrive_MyDrive/GitHub/admiral-development/admiral")
library(devtools)
# Make some changes in R/my_first_fcn.R
devtools::document()
ℹ Updating admiral documentation
ℹ Loading admiral
```

When you run devtools::document(), it:
1. Reads the roxygen2 comments (lines starting with #') from your R script (e.g., admiral-development\admiral\R\my_first_fcn.R).
2. Converts those comments into a .Rd file (if it doesn't already exist) or updates the corresponding .Rd file (e.g., admiral-development\admiral\man\my_first_fcn.Rd) to reflect any changes in the documentation.

### Roxygen check failed
[Closes #2593 feat: Add my_first_fcn to welcome new users #3946](https://github.com/pharmaverse/admiral/actions/runs/12172770986/job/33952042039?pr=2593)

Run git status -s
 M NAMESPACE
?? man/my_first_fcn.Rd
🙈 Manuals are not up-to-date with roxygen comments!
🔀 The following differences were noted:

💻 Please rerun the following command on your workstation and push your changes
--------------------------------------------------------------------
roxygen2::roxygenize('.', roclets = c('rd', 'collate', 'namespace'))
--------------------------------------------------------------------
ℹ roxygen2 version that was used in this workflow: ‘7.3.2’
🙏 Please ensure that the 'RoxygenNote' field in the DESCRIPTION file matches this version
Error: Process completed with exit code 1.

### What is the NAMESPACE file?
The NAMESPACE file in an R package is an essential file that controls which functions, datasets, and objects are made available to users and other packages. It plays a crucial role in defining the interface of the package—what is exposed to the user and what remains internal (hidden). It also governs how functions are imported from other packages.

### Roxygen2 and the NAMESPACE File
When you use Roxygen2 to document your package, it automatically generates and updates the NAMESPACE file based on the comments (like @export, @import, and @importFrom) in your R scripts. For example:

Exporting a Function: In the R function file (e.g., my_first_fcn.R), you can add the following Roxygen2 comment to indicate that the function should be exported:
```r
#' @export
my_first_fcn <- function() {
  "Welcome to admiral!"
}
```
The NAMESPACE file will be updated as
```r
export(my_first_fcn)
```

### What is the DESCRIPTION file?
The DESCRIPTION file contains essential metadata about your package, including its name, version, dependencies, and other key details. While it may not be directly related to the issue you’re seeing with NAMESPACE, it’s still crucial to update it and push it whenever there are changes that affect the package structure or dependencies.

### Key Differences Between roxygen2::roxygenize() and devtools::document()
`roxygen2::roxygenize()`
1. Primary Purpose: The roxygenize() function from the roxygen2 package is directly responsible for processing your R scripts, extracting Roxygen comments, and generating the corresponding documentation files (.Rd files) and updating the NAMESPACE file.

2. What It Does:
* It updates .Rd files in the man/ directory.
* It updates the NAMESPACE file based on @export tags.
* It generates any other documentation required (e.g., collate order, namespace).
* If you have any custom Roxygen configurations or if you want to specify which "roclets" to use (like rd, collate, or namespace), roxygenize() gives you more granular control.

`devtools::document()`
1. Primary Purpose: The document() function from the devtools package is a more general-purpose function, and it automates many tasks related to package development, including documentation.

2. What It Does:
* It calls roxygen2::roxygenize() internally to regenerate documentation.
* It also reloads the package in the environment (if you are working interactively) and ensures the generated documentation is used in the current R session.
* It handles more package-related tasks like checking the internal structure of the package and reloading certain files (e.g., updating .Rbuildignore, DESCRIPTION file), and sometimes it may perform additional checks that aren't strictly related to documentation alone.

### roxygen2::roxygenize('.', roclets = c('rd', 'collate', 'namespace'))
Given that your current working directory (getwd()) is set to the package root (C:/GoogleDrive_MyDrive/GitHub/admiral-development/admiral), you should run the following command:
```r
roxygen2::roxygenize('.', roclets = c('rd', 'collate', 'namespace'))
#ℹ Loading admiral
```

## Update NEWS.md
Update NEWS.md under the header # admiral (development version) if the changes pertain to a user-facing function (i.e. it has an @export tag) or documentation aimed at users (rather than developers). A Developer Notes section is available in NEWS.md for tracking developer-facing issues. 

To update the NEWS.md according to the feedback, follow these steps:

1. Choose the Relevant Section
Based on the type of changes you've made, determine the appropriate section in the NEWS.md file:

**New Features**: If your changes introduce new functionality or new functions.
**Updates of Existing Functions**: If you made improvements or modifications to an existing function (e.g., your my_first_fcn function).
**Breaking Changes**: If your changes introduce any changes that would break backward compatibility.
**Documentation**: If your changes are mainly related to documentation updates or new docstrings.
In your case, since you've modified the documentation and function description, the Documentation section seems most appropriate.

2. Format Your Entry
The format for your entry should be short, informative, and consistent with previous entries. You also need to include the issue number if applicable. Here's an example based on the feedback:
```markdown
### Documentation

- Updated the documentation for `my_first_fcn()` to improve the clarity of the `@return` description, now stating: "A string with a welcome message 'Welcome to admiral!'". (#2593)
```

## push the changes to the admiral repository on GitHub
```bash
cd C:/GoogleDrive_MyDrive/GitHub/admiral-development/admiral
```
Branch: (feature/my_first_fcn), meaning you're on the feature/my_first_fcn branch, which is the branch you're working on.

Your git push to the branch feature/my_first_fcn is directly tied to the pull request (PR) #2593 because the PR is associated with that specific branch in your fork of the repository. Here's how it works:

1. PR Branch Tracking: When you create a PR on GitHub, you specify:
* The source branch (e.g., feature/my_first_fcn in your fork).
* The target branch (e.g., main or dev in the pharmaverse/admiral repo).
The PR links these branches and tracks changes made to the source branch (feature/my_first_fcn).

2. Git Push Updates the PR: Each time you git push changes to the branch associated with the PR (feature/my_first_fcn in this case), GitHub automatically updates the PR to reflect those changes.

This means any commits you push will:

* Be visible in the "Commits" tab of the PR.
* Trigger automated checks (like CI/CD pipelines) if they are set up for the repository.
* Allow reviewers to see your latest updates.

3. How It Works for #2593:

* Your PR #2593 is associated with the feature/my_first_fcn branch.
* By running git push origin feature/my_first_fcn, you're sending the latest changes in your local branch to the remote repository on GitHub.
* GitHub updates PR #2593 automatically to include these changes.

4. Finalizing the PR: Once your changes are reviewed and approved, a maintainer or you (if you have the necessary permissions) will merge the PR into the target branch (e.g., main or dev).

```bash
git status

#Changes not staged for commit:
#  (use "git add <file>..." to update what will be committed)
#  (use "git restore <file>..." to discard changes in working directory)
#        modified:   NAMESPACE
#        modified:   NEWS.md
#        modified:   R/my_first_fcn.R
		
#Untracked files:
#  (use "git add <file>..." to include in what will be committed)
#        man/my_first_fcn.Rd
#        tests/testthat/_snaps/derive_extreme_event.new.md
#        tests/testthat/_snaps/derive_param_tte.new.md
#        tests/testthat/_snaps/derive_var_dthcaus.new.md
#        tests/testthat/_snaps/derive_var_extreme_date.new.md
#        tests/testthat/_snaps/derive_var_merged_ef_msrc.new.md
```
Modified Files
NAMESPACE, NEWS.md, R/my_first_fcn.R: These are expected since they are part of your changes.

Untracked Files
man/my_first_fcn.Rd: The documentation for my_first_fcn, created by running roxygen2::roxygenize() or devtools::document().
New .new.md files in tests/testthat/_snaps: Generated by running tests, likely because new or updated tests were added that produce new outputs

You should include all the files relevant to your feature and documentation updates, but you might not need to include some testing-related files unless those updates are intentional or required for your feature.

Step 1: Stage the Relevant Files
Stage the files you want to include in your commit:
```bash
git add NAMESPACE NEWS.md R/my_first_fcn.R man/my_first_fcn.Rd
# warning: in the working copy of 'man/my_first_fcn.Rd', LF will be replaced by CRLF the next time Git touches it
```
The warning indicates that Git is handling differences in line endings between your operating system and the repository's configuration.

What This Means
* LF (Line Feed): Used in Unix/Linux and macOS systems for line breaks.
* CRLF (Carriage Return + Line Feed): Used in Windows systems for line breaks.

This warning appears because:
1. You are likely on a Windows system.
2. The .gitattributes file in the repository specifies how line endings should be normalized (e.g., converting LF to CRLF for Windows or keeping LF universally).
Git is warning you that it will convert the file's line endings to match the repository's settings the next time you modify the file. You can continue with your git commit and git push as usual. This warning should not block your workflow:

```bash
git commit -m "Add my_first_fcn implementation and update documentation, NAMESPACE, and NEWS.md"
#[feature/my_first_fcn 9f3ca92a7] Add my_first_fcn implementation and #update documentation, NAMESPACE, and NEWS.md
# 4 files changed, 19 insertions(+), 2 deletions(-)
# create mode 100644 man/my_first_fcn.Rd

git push origin feature/my_first_fcn
#Enumerating objects: 14, done.
#Counting objects: 100% (14/14), done.
#Delta compression using up to 20 threads
#Compressing objects: 100% (8/8), done.
#Writing objects: 100% (8/8), 1.07 KiB | 1.07 MiB/s, done.
#Total 8 (delta 6), reused 0 (delta 0), pack-reused 0 (from 0)
#remote: Resolving deltas: 100% (6/6), completed with 6 local objects.
#To https://github.com/pharmaverse/admiral.git
#   1171f22c0..9f3ca92a7  feature/my_first_fcn -> feature/my_first_fcn
```