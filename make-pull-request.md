## pull request
[DUMMY ISSUE FOR ONBOARDING #1839](https://github.com/pharmaverse/admiral/issues/1839)
Please create a new function my_first_fcn() that outputs "Welcome to the admiral family!".

You can use this dummy issue to follow our development process up to the point the pull request is ready to be merged, and then we would close and delete the feature branch, as this is just for practice and not a real contribution needed.

## Steps Without Forking
If you don’t see a Fork button, it may be because you have direct write access to the repository (e.g., you're a collaborator). In that case, you can follow these adjusted steps:

Change working directory
```bash
cd C:/GoogleDrive_MyDrive/GitHub/admiral-development
```
Clone the Repository
Clone the main repository directly to your local machine:
```bash
git clone https://github.com/pharmaverse/admiral.git
```

Navigate to the repository:
```bash
cd admiral
```

Create a New Branch
Create and switch to a new feature branch:
```bash
git checkout -b feature/my_first_fcn
#Switched to a new branch 'feature/my_first_fcn'
```

Follow the steps outlined earlier to:
* Create the function in a new file, such as R/my_first_fcn.R
creating the my_first_fcn.R file in the R folder is the correct choice because this folder is typically where the core functions of an R package are stored
```r
#' My First Function
#'
#' This function outputs a welcome message for onboarding purposes.
#'
#' @return A string with a welcome message.
#' @export
#'
my_first_fcn <- function() {
  "Welcome to the admiral family!"
}
```
## Document the function using devtools::document().
* Navigate to Your Project Root: Ensure you're in the root directory of your package (where the DESCRIPTION file is located)
```r
setwd("C:/GoogleDrive_MyDrive/GitHub/admiral-development/admiral")
getwd()
# [1] "C:/GoogleDrive_MyDrive/GitHub/admiral-development/admiral"
```
* Run devtools::document(). This command:
Reads your Roxygen2 comments (like @param, @return, etc.) in my_first_fcn.R.
Generates or updates .Rd files in the man/ directory for your function.
Updates the NAMESPACE file to include your function if you've used @export.
```r
devtools::document()
#ℹ Updating admiral documentation
#ℹ Loading admiral
#Writing NAMESPACE
#Writing my_first_fcn.Rd
```
* Verify Documentation: Check the generated documentation:
Open the .Rd file for your function in the man/ folder. The file path is "C:\GoogleDrive_MyDrive\GitHub\admiral-development\admiral\man\my_first_fcn.Rd"

In RStudio, use ?my_first_fcn to confirm the documentation appears as expected.

## Add a Test Case
Navigate to the folder for tests:
C:\GoogleDrive_MyDrive\GitHub\admiral-development\admiral\tests\testthat

Create a New Test File: test-my_first_fcn.R

Open the file and add the following:
```r
test_that("my_first_fcn works correctly", {
    result <- my_first_fcn()
    expect_type(result, "character")  # Test that the output is a string
    expect_equal(result, "Welcome to the admiral family!")  # Test the exact content
})
```
Save the File.

## Run the Tests
Ensure testthat is Installed: Run this in your R console if not already installed:
```r
install.packages("diffdf")
install.packages("testthat")
```

Run All Tests: In your R console or script, run:
```r
devtools::test()
```

When running devtools::test() across an entire package, it's normal to see errors or failures from existing tests that are part of the package's test suite. If these errors are not related to the changes you've made, you can generally ignore them.
However, to ensure your changes haven't introduced new issues, you should:

Look specifically at the tests related to your new function
Ensure your new tests pass
Check that you haven't inadvertently broken existing functionality

If you want to run only the tests you've added, you can use:
```r
devtools::test(filter = "my_first_fcn")
#ℹ Testing admiral
#✔ | F W  S  OK | Context
#✔ |          2 | #my_first_fcn                                                               # ══ Results #══════════════════════════════════════════════════════════════════════════
#[ FAIL 0 | WARN 0 | SKIP 0 | PASS 2 ]
#Warning message:
#── Conflicts #───────────────────────────────────────────────────────────────────────────#─────── admiral conflicts──
#✖ `my_first_fcn` masks `admiral::my_first_fcn()`.
#ℹ Did you accidentally source a file rather than using `load_all()`?
#  Run `rm(list = c("my_first_fcn"))` to remove the conflicts. 
```

## Differences between `my_first_fcn` and `admiral::my_first_fcn`
Let me break this down:

my_first_fcn (without ::)

This is the function you created in your local R environment
It's typically defined directly in the R script you wrote
When used without ::, it refers to the function as a local/global environment object


admiral::my_first_fcn() (with ::)

This is the function as it exists within the admiral package namespace
The :: syntax explicitly calls the function from the admiral package
This suggests there might already be a function with this name in the admiral package

The warning you saw indicates that the function you created is masking (overriding) the package's existing function.

## Resolve conflict between `my_first_fcn` and `admiral::my_first_fcn()`
The warning message `my_first_fcn` masks `admiral::my_first_fcn()` suggests that there might be a conflict with an existing my_first_fcn() function in the package. This can happen if you've accidentally sourced the file directly instead of using devtools::load_all().
To resolve this, try the following steps:

First, remove the conflicting function:
```r
rm(list = c("my_first_fcn"))
```

Then, use devtools::load_all() instead of sourcing the file directly:
```r
devtools::load_all()
# ℹ Loading admiral
```

Run the tests again:
```r
devtools::test(filter = "my_first_fcn")
#ℹ Testing admiral
#✔ | F W  S  OK | Context
#✔ |          2 | my_first_fcn
══Results═══════════════════════════════════════════════════════════════════
[ FAIL 0 | WARN 0 | SKIP 0 | PASS 2 ]
```
the test for my_first_fcn() would be located in a test file, typically at tests/testthat/test-my_first_fcn.R.

When you run devtools::test(filter = "my_first_fcn"), it specifically looks for and runs tests that match this pattern. The output shows:

```r
✔ |          2 | my_first_fcn
```

## Stage your changes:
```bash
git add R/my_first_fcn.R
git add tests/testthat/test-my_first_fcn.R
```

## Commit your changes:
```bash
git commit -m "feat: Add my_first_fcn to welcome new users
- Create new function my_first_fcn()
- Add corresponding test
- Resolves #1839"
```

## Push your branch to your fork:
```bash
git push -u origin feature/my_first_fcn
#Enumerating objects: 11, done.
#Counting objects: 100% (11/11), done.
#Delta compression using up to 20 threads
#Compressing objects: 100% (7/7), done.
#Writing objects: 100% (7/7), 918 bytes | 918.00 KiB/s, done.
#Total 7 (delta 3), reused 0 (delta 0), pack-reused 0 (from 0)
#remote: Resolving deltas: 100% (3/3), completed with 3 local objects.
#remote:
#remote: Create a pull request for 'feature/my_first_fcn' on GitHub by #visiting:
#remote:      https://github.com/pharmaverse/admiral/pull/new/feature/my_first_fcn
#remote:
To https://github.com/pharmaverse/admiral.git
#* [new branch]          feature/my_first_fcn -> feature/my_first_fcn
#branch 'feature/my_first_fcn' set up to track 'origin/feature/my_first_fcn'.
```

## Check the pull request page
On the pull request page, search for other pull requests with a similar name (feature/my_first_fcn) or check for multiple PRs related to the same issue.
If the issue is about a specific function, it's likely that other contributors might have worked on the same functionality, so look for any conflicting PRs.

If you're unable to see #1839 on the pull request page of the repository, it could be due to a few reasons. Here are some steps to help troubleshoot:

1. Check if Your Pull Request Was Created
After pushing your changes to the branch, you need to manually create a pull request. If you haven’t done so yet, GitHub won’t automatically create the PR for you.
To create the pull request:
* Go to the repository’s Pull Requests page.
* Click the "New Pull Request" button.
* Select your branch (e.g., feature/my_first_fcn) and the base branch you want to merge it into (usually main or develop).
* Add a title and description, referencing the issue #1839 in the description.
* Click "Create Pull Request".

At https://github.com/pharmaverse/admiral/compare/main...feature/my_first_fcn I can see  Able to merge. These branches can be automatically merged. Can I simply click on Create pull request?

Yes, if you see "Able to merge. These branches can be automatically merged." on the comparison page (https://github.com/pharmaverse/admiral/compare/main...feature/my_first_fcn), that means there are no merge conflicts between your branch (feature/my_first_fcn) and the base branch (main).

You can safely click on "Create pull request" to finalize and submit your pull request. Here's a quick checklist to ensure everything is ready:

Add a title
feat: Add my_first_fcn to welcome new users

Add a description
- Create new function my_first_fcn()
- Add corresponding test
- Resolves #1839

Thank you for your Pull Request! We have developed this task checklist from the [Development Process Guide](https://pharmaverse.github.io/admiral/CONTRIBUTING.html#detailed-development-process) to help with the final steps of the process. Completing the below tasks helps to ensure our reviewers can maximize their time on your code as well as making sure the admiral codebase remains robust and consistent.   

Please check off each taskbox as an acknowledgment that you completed the task or check off that it is not relevant to your Pull Request. This checklist is part of the Github Action workflows and the Pull Request will not be merged into the `main` branch until you have checked off each task.

- [ ] Place Closes #<insert_issue_number> into the beginning of your Pull Request Title (Use Edit button in top-right if you need to update)
- [ ] Code is formatted according to the [tidyverse style guide](https://style.tidyverse.org/). Run `styler::style_file()` to style R and Rmd files
- [ ] Updated relevant unit tests or have written new unit tests, which should consider realistic data scenarios and edge cases, e.g. empty datasets, errors, boundary cases etc. - See [Unit Test Guide](https://pharmaverse.github.io/admiraldev/articles/unit_test_guidance.html#tests-should-be-robust-to-cover-realistic-data-scenarios)
- [ ] If you removed/replaced any function and/or function parameters, did you fully follow the [deprecation guidance](https://pharmaverse.github.io/admiraldev/articles/programming_strategy.html#deprecation)?
- [ ] Review the [Cheat Sheet](https://github.com/pharmaverse/admiral/blob/main/inst/cheatsheet/admiral_cheatsheet.pdf). Make any required updates to it by editing the file `inst/cheatsheet/admiral_cheatsheet.pptx` and re-upload a PDF and a PNG version of it to the same folder. (The PNG version can be created by taking a screenshot of the PDF version.)
- [ ] Update to all relevant roxygen headers and examples, including keywords and families. Refer to the [categorization of functions](https://pharmaverse.github.io/admiraldev/articles/programming_strategy.html#categorization-of-functions) to tag appropriate keyword/family.
- [ ] Run `devtools::document()` so all `.Rd` files in the `man` folder and the `NAMESPACE` file in the project root are updated appropriately
- [ ] Address any updates needed for vignettes and/or templates
- [ ] Update `NEWS.md` under the header `# admiral (development version)` if the changes pertain to a user-facing function (i.e. it has an `@export` tag) or documentation aimed at users (rather than developers). A Developer Notes section is available in `NEWS.md` for tracking developer-facing issues.  
- [ ] Build admiral site `pkgdown::build_site()` and check that all affected examples are displayed correctly and that all new functions occur on the "[Reference](https://pharmaverse.github.io/admiral/reference/index.html)" page. 
- [ ] Address or fix all lintr warnings and errors - `lintr::lint_package()`
- [ ] Run `R CMD check` locally and address all errors and warnings - `devtools::check()`
- [ ] Link the issue in the Development Section on the right hand side.
- [ ] Address all merge conflicts and resolve appropriately
- [ ] Pat yourself on the back for a job well done! Much love to your accomplishment!
