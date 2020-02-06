
<!-- README.md is generated from README.Rmd. Please edit that file -->

# pli

<!-- badges: start -->

[![R build
status](https://github.com/illinois-r/pli/workflows/R-CMD-check/badge.svg)](https://github.com/illinois-r/pli)
<!-- badges: end -->

The goal of pli is to provide an interface to [PrairieLearn’s API
endpoints](https://prairielearn.readthedocs.io/en/latest/api/).

## Installation

You can install the released version of pli from
[GitHub](https://github.com/illinois-r/pli) with:

``` r
if(!requireNamespace("devtools")) { install.packages("devtools") }
devtools::install_githu("illinois-r/pli")
```

## Setup

Prior to using `pli`, you must create a personal access token on
PrairieLearn’s production server.

<https://prairielearn.engr.illinois.edu/pl/settings>

Once on the page, press “(+) Generate New Token”. The token will only be
displayed only once. Please make sure to copy the token.

For *R* to know about the token, please include it in your `.Renviron`
file.

Open the `~/.Renviron` file by typing:

``` r
usethis::edit_r_environ()
```

Inside the file, add the following line:

``` bash
PRAIRIELEARN_API_TOKEN="<your-token-here>"
```

Subsitute `<your-token-here>` with the token that was generated.
(**Note:** Make sure to remove `<>`.)

## Endpoints

We presently support:

| Function                          | Description                                             |
| --------------------------------- | ------------------------------------------------------- |
| `pl_course_gradebook()`           | Gradebook                                               |
| `pl_assessment_list()`            | List of all assessments in course                       |
| `pl_assessment_view()`            | View a single assessment in course                      |
| `pl_assessment_instance_list()`   | List of all instances underneath a specific assessment  |
| `pl_assessment_instance_view()`   | View a single student instances of an assessment        |
| `pl_assessment_submission_list()` | List of all submission underneath a specific assessment |
| `pl_assessment_submission_view()` | View a single student submission                        |
