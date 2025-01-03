## Issue #2551 
The files derive_adeg_parms.R and derive_advs_parms.R should be restructured such that there is one file per "parameter". E.g., derive_param_qtc.R contains derive_param_qtc() and compute_qtc().
The test files should be restructured accordingly.

## Definition of Done
derive_adeg_parms.R and derive_advs_parms.R and their test files are replaced.

## Split files 

Original File			Function			New File
---------------------------------------------------------------
derive_adeg_params.R	derive_param_qtc	derive_param_qtc.R
derive_adeg_params.R	default_qtc_paramcd	derive_param_qtc.R
derive_adeg_params.R	compute_qtc			derive_param_qtc.R
derive_adeg_params.R	derive_param_rr		derive_param_rr.R
derive_adeg_params.R	compute_rr			derive_param_rr.R
------------------------	----------------------	-----------
derive_advs_params.R	derive_param_map	derive_param_map.R
derive_advs_params.R	compute_map			derive_param_map.R
derive_advs_params.R	derive_param_bsa	derive_param_bsa.R
derive_advs_params.R	compute_bsa			derive_param_bsa.R
derive_advs_params.R	derive_param_bmi	derive_param_bmi.R
derive_advs_params.R	compute_bmi			derive_param_bmi.R
---------------------------------------------------------------

| Original File                            | New File                              |
|------------------------------------------|---------------------------------------|
| tests/testthat/test-derive_adeg_params.R | tests/testthat/test-derive_param_qtc.R |
| tests/testthat/test-derive_adeg_params.R | tests/testthat/test-derive_param_rr.R  |
| tests/testthat/test-derive_advs_params.R | tests/testthat/test-derive_param_bmi.R |
| tests/testthat/test-derive_advs_params.R | tests/testthat/test-derive_param_bsa.R |
| tests/testthat/test-derive_advs_params.R | tests/testthat/test-derive_param_map.R |

## Update .Rd files
```r
setwd("C:/GoogleDrive_MyDrive/GitHub/admiral-development/admiral")
styler::style_file(c("R/derive_param_qtc.R","R/derive_param_rr.R","R/derive_param_map.R","R/derive_param_bmi.R","R/derive_param_bsa.R"))

Styling  5  files:
 R/derive_param_qtc.R ✔ 
 R/derive_param_rr.R  ✔ 
 R/derive_param_map.R ✔ 
 R/derive_param_bmi.R ✔ 
 R/derive_param_bsa.R ✔ 
────────────────────────────────────────
Status	Count	Legend 
✔ 	5	File unchanged.
ℹ 	0	File changed.
✖ 	0	Styling threw an error.
────────────────────────────────────────
```

```r
> devtools::document()
ℹ Updating admiral documentation
ℹ Loading admiral
Error in `load_all()`:
! Failed to load R/tte_sources.R
Caused by error in `assert_character_scalar()`:
! could not find function "assert_character_scalar"
Run `rlang::last_trace()` to see where the error occurred.
Warning message:
In loadNamespace(i, c(lib.loc, .libPaths()), versionCheck = vI[[i]]) :
  namespace ‘admiraldev’ 1.1.0 is already loaded, but >= 1.1.0.9007 is required
```
The error you're seeing, could not find function "assert_character_scalar", indicates that the function assert_character_scalar is not available, which may be due to a missing or incompatible package version.

Steps to resolve:
1. Check if rlang is properly installed and up to date
The assert_character_scalar function is part of the rlang package. It’s possible that the version of rlang installed is outdated or incompatible with the code you're trying to run. You can update rlang to the latest version:

2. Run R as Administrator
Since the error message involves permission issues, try running R (or RStudio) with elevated privileges:

For RStudio: Right-click on the RStudio icon and select "Run as administrator."
For R Console: Open the command prompt as an administrator and then start R from there by typing R.
After running R as an administrator, try reinstalling rlang again:
```r
install.packages("rlang")
```

```r
setwd("C:/GoogleDrive_MyDrive/GitHub/admiral-development/admiral")
devtools::document()
ℹ Updating admiral documentation
ℹ Loading admiral
Writing derive_param_qtc.Rd
Writing default_qtc_paramcd.Rd
Writing compute_qtc.Rd
Writing derive_param_rr.Rd
Writing compute_rr.Rd
Writing derive_param_map.Rd
Writing compute_map.Rd
Writing derive_param_bsa.Rd
Writing compute_bsa.Rd
Writing derive_param_bmi.Rd
Writing compute_bmi.Rd
```
The reason for generating 11 .Rd files is that your R scripts likely contain multiple functions, some of which may also be documented, either as exported functions or internal functions. As a result, devtools::document() is creating .Rd files for each documented function, not just the 5 R files themselves.

```r
roxygen2::roxygenize('.', roclets = c('rd', 'collate', 'namespace'))
ℹ Loading admiral
```

## Stage changes
```bash
cd C:/GoogleDrive_MyDrive/GitHub/admiral-development/admiral
git add .
git commit -m "Add new R files, test files, and documentation for issue #2551"
git push origin feature/my_first_fcn
```

## Questions and response
Some questions:

Does the test numbering in the test-*.R files always need to start at 1? For example, in test-derive_param_rr.R, the test headings currently begin at 5 as its original file:

>> Yes! If you are restructuring tests or updating old ones it is good to re-number the Tests. You can install this addin from github pharmaverse4devs to help with renumbering

https://pharmaverse.github.io/admiraldev/dev/articles/unit_test_guidance.html#addin-pharmaverse4devsformat_test_that_file

"## Test 5: new observations are derived correctly" 
"## Test 6: Message if no new records" Should these be renumbered to start at Test 1 and Test 2?

>> Yes! Use the addin as it is super quick and easy. We like our bureaucracy in admiral!

Should I delete the original files to avoid redundancy? These include:
derive_adeg_params.R
derive_advs_params.R
test-derive_adeg_params.R
test-derive_advs_params.R
>> Yes please remove these files - good to run local devtools::check() but the GHA will also pick up any issues

Should the following R commands be run whenever files are created, deleted, or edited?
styler::style_file()
devtools::document()
roxygen2::roxygenize('.', roclets = c('rd', 'collate', 'namespace'))
>> The first two - I think the third is needed if multiple people are using different versions of the roxygen and the GHAs checks get confused and recommends it. Maybe others know why @pharmaverse/admiral

### Step 1: Install and Load Necessary Packages
```r
    if (!requireNamespace("remotes", quietly = TRUE)) {
      install.packages("remotes")
    }
    remotes::install_github("pharmaverse/pharmaverse4devs")
# Load the package
library(pharmaverse4devs)
```
### Run RStudio as Admin
Closed RStudio and reopened it using  Run As Admin. Select `Format test_that test file` from Addins button

### Step 2: Open a test file and run `Format test_that test file`
```r
setwd("C:/GoogleDrive_MyDrive/GitHub/admiral-development/admiral")
```
Open one of these `test-*.R` files last modified datetime on 21Dec2024 in RStudio
tests/testthat/test-derive_param_bmi.R
tests/testthat/test-derive_param_map.R
tests/testthat/test-derive_param_qtc.R
tests/testthat/test-derive_param_rr.R
tests/testthat/test-derive_param_bsa.R

Scroll to the very end of the file and check if the cursor is at the last character or if there's an empty line.

Select `Format test_that test file` from Addins button

If the last line is an empty line, it will be removed

Test headings will be renumbered from 1

### Remove old files
R/derive_adeg_params.R
R/derive_advs_params.R
tests/testthat/test-derive_adeg_params.R
tests/testthat/test-derive_advs_params.R
```r
getwd()
#[1] "C:/GoogleDrive_MyDrive/GitHub/admiral-development/admiral"

# Specify the paths of the files you want to delete
files_to_delete <- c(
  "R/derive_adeg_params.R",
  "R/derive_advs_params.R",
  "tests/testthat/test-derive_adeg_params.R",
  "tests/testthat/test-derive_advs_params.R"
)

# Delete the files
file.remove(files_to_delete)
#[1] TRUE TRUE TRUE TRUE
```

### Run `styler::style_file()` `devtools::document()`  
Run these R functions after creating, editing, deleting files
`styler::style_file()`
`devtools::document()`

```r
setwd("C:/GoogleDrive_MyDrive/GitHub/admiral-development/admiral/tests/testthat/")

# Style new files
styler::style_file(c("test-derive_param_bmi.R","test-derive_param_map.R","test-derive_param_qtc.R","test-derive_param_rr.R","test-derive_param_bsa.R"))

Styling  5  files:
 test-derive_param_bmi.R ℹ 
 test-derive_param_map.R ℹ 
 test-derive_param_qtc.R ℹ 
 test-derive_param_rr.R  ℹ 
 test-derive_param_bsa.R ℹ 
────────────────────────────────────────
Status	Count	Legend 
✔ 	0	File unchanged.
ℹ 	5	File changed.
✖ 	0	Styling threw an error.
────────────────────────────────────────
Please review the changes carefully!

devtools::document()
ℹ Updating admiral documentation
ℹ Loading admiral
Writing derive_param_bmi.Rd
Writing compute_bmi.Rd
Writing derive_param_bsa.Rd
Writing compute_bsa.Rd
Writing derive_param_map.Rd
Writing compute_map.Rd
Writing derive_param_qtc.Rd
Writing default_qtc_paramcd.Rd
Writing compute_qtc.Rd
Writing derive_param_rr.Rd
Writing compute_rr.Rd
```

### Commit and Push Changes to feature/my_first_fcn Branch
```bash
cd C:/GoogleDrive_MyDrive/GitHub/admiral-development/admiral
git add .
git commit -m "Deleted unused test and R scripts, formatted 5 test_that test files"
#[feature/my_first_fcn 76def67c2] Deleted unused test and R scripts, formatted 5 test_that test #files
# 20 files changed, 131 insertions(+), 3268 deletions(-)
# delete mode 100644 R/derive_adeg_params.R
# delete mode 100644 R/derive_advs_params.R
# delete mode 100644 tests/testthat/test-derive_adeg_params.R
# delete mode 100644 tests/testthat/test-derive_advs_params.R

git push origin feature/my_first_fcn
```
