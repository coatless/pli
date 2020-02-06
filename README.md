
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

## Sample workflow

First, login in to PrairieLearn and select the course you wish to obtain
information from. The course instance number for this course can be
obtained by looking at the URL for the class:

    https://prairielearn.engr.illinois.edu/pl/course_instance/54777/instructor/instance_admin/assessments

In this case, the course instance number would be `54777`. With this in
hand, let’s query the grade book:

``` r
library(pli)
course_instance_id = 54777

## Gradebook Manipulations ---- 

# Download the entire gradebook
grades = pl_course_gradebook(course_instance_id)


# Format for a single assessment to Compass2g
library(tidyverse)
grades %>% 
  filter(assessment_id == 1228980) %>%
  select(user_uid, points) %>%
  mutate(
         points = replace_na(points, 0),
         user_uid = gsub("@.*","", user_uid)
        ) %>%
  write_csv("grades-quiz1.csv")

## Specific assessment manipulation ----

# Get an overview of all assessments
assessments = pl_assessment_list(course_instance_id)

# Retrieve scores for that instance
quiz_1 = pl_assessment_instance_list(course_instance_id, 1228980)

# Export to Compass2g
grade_format_compass2g(quiz_1, "quiz1-stat486.csv")
```
