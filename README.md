
<!-- README.md is generated from README.Rmd. Please edit that file -->

# grkstyle

<!-- badges: start -->

[![grkstyle status
badge](https://gadenbuie.r-universe.dev/badges/grkstyle)](https://gadenbuie.r-universe.dev)
[![R-CMD-check](https://github.com/gadenbuie/grkstyle/actions/workflows/R-CMD-check.yaml/badge.svg)](https://github.com/gadenbuie/grkstyle/actions/workflows/R-CMD-check.yaml)
<!-- badges: end -->

`grkstyle` is an extension package for
[styler](https://styler.r-lib.org) that holds my personal code style
preferences.

## Installation

You can install grkstyle from my
[r-universe](https://gadenbuie.r-universe.dev):

``` r
options(repos = c(
	gadenbuie = "https://gadenbuie.r-universe.dev",
	getOptions("repos")
))

# Download and install grkstyle in R
install.packages("grkstyle")
```

Or you can install grkstyle directly from Github:

``` r
# install.packages("remotes")
remotes::install_github("gadenbuie/grkstyle")
```

## Usage

To use `grkstyle` by default in styler functions and addins

``` r
# Set default code style for {styler} functions
grkstyle::use_grk_style()
```

Or add the following to your `~/.Rprofile`

    options(styler.addins_style_transformer = "grkstyle::grk_style_transformer()")

## Examples

A few examples drawn from the [tidyverse style
guide](https://style.tidyverse.org).

### Tabs vs Spaces

I’ve been staunchly committed to indentation by two spaces, but I’ve
recently come to realize that indentation with tabs is objectively
better. Primarily [it’s about
accessibility](https://alexandersandberg.com/articles/default-to-tabs-instead-of-spaces-for-an-accessible-first-environment/).
Using tabs allows others to choose their preferred indentation levels,
it accommodates more code authors in a wider variety of scenarios, and
it’s better for Braille code readers:

> The main reason I would like to see this change is for refreshable
> braille displays that are used by blind programmers a lot. Each space
> wastes one braille cell and takes away valuable braille realestate. So
> if the default indentation of a project is 4 spaces per level, a 3rd
> level indentation wastes 12 braille cells before code starts.  
> —
> [Comment](https://github.com/prettier/prettier/issues/7475#issuecomment-668544890)
> by [MarcoZehe](https://github.com/MarcoZehe)

All of the `grk_style_text()`, `grk_style_file()`, `grk_style_dir()` and
`grk_style_pkg()` functions will by default automatically detect the
`UseTabsForSpaces` setting the RStudio project file. You can switch to
tabs by updating the RStudio project settings to disable “Insert spaces
for tab” (Tools \> Project Options \> Code Editing \> *Insert spaces for
tab*) and then running one of the above functions. Alternatively, you
can set `grkstyle.use_tabs = TRUE` in the `.Rprofile` file in your home
directory or your project directory.

**unstyled**

``` r
fruits <- c(
  "apple",
  "banana",
  "mango"
)
```

**grkstyle**

``` r
fruits <- c(
	"apple",
	"banana",
	"mango"
)
```

If you’d like to quickly transition **to tabs** throughout your package
code, you can use the `grk_reindent_tabs_*()` helper functions. These
function apply *only* the styler indentation rules and should only
affect the indentation of your code.

``` r
# re-indent your package code using tabs
grk_reindent_tabs_pkg()
```

There are equivalent helper functions to standardize around spaces,
e.g. `grk_reindent_spaces_*()`, or to use the RStudio project option,
e.g. `grk_reindent_auto_*()`.

### Line Breaks Inside Function Calls

**unstyled**

``` r
do_something_very_complicated(something = "that", requires = many,
                              arguments = "some of which may be long")
```

**grkstyle**

``` r
do_something_very_complicated(
	something = "that",
	requires = many,
	arguments = "some of which may be long"
) 
```

**styler::tidyverse_style**

``` r
do_something_very_complicated(
  something = "that", requires = many,
  arguments = "some of which may be long"
) 
```

### Indentation of Function Arguments

**unstyled**

``` r
long_function_name <- function(a = "a long argument",
                               b = "another argument",
                               c = "another long argument") {
  # As usual code is indented by two spaces.
}
```

**grkstyle**

``` r
long_function_name <- function(
	a = "a long argument",
	b = "another argument",
	c = "another long argument"
) {
	# As usual code is indented by two spaces.
} 
```

**styler::tidyverse_style**

``` r
long_function_name <- function(a = "a long argument",
                               b = "another argument",
                               c = "another long argument") {
  # As usual code is indented by two spaces.
} 
```
