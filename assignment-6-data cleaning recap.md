---
title: "Data Cleaning Recap: Do it Yourself"
author: "Lucas Ambrose""
output: html_document
---

# Assignment-6 - Data Cleaning Recap

Put everything together from scratch! Create a new repo in github, create a README file that has a description of what you will be doing, and then an rmd file to harbor your code. You will be completing one of the "your turn" tasks from the lectures

# Your Turn Task

During the 1870 census data on people's occupation was collected. The data [occupation-1870](https://srvanderplas.github.io/rwrks/03-r-format/data/occupation-1870.csv) contains state-level aggregates of occupation by gender.

-   Use `tidyr` to get the data into a long format (use `pivot_longer`).

-   Separate the `occupation.gender` type variable into two variables.

-   "Spread" (use `pivot_wider`) the data such that you can draw scatterplots of values for men against women facetted by occupation.

```{r}
library(tidyr)
library(dbplyr)
library(stringr)
library(ggplot2)
occupation <- read.csv("occupation-1870.csv")
occupation_long <- occupation %>%
  pivot_longer(-c("Area.name", "Total.Population"), names_to = "Occupation", values_to = "Measurement") %>%
  separate_wider_delim(Occupation, delim = ".", names = c("Occupation","Gender")) %>%
  pivot_wider(names_from = "Gender", values_from = "Measurement")
head(occupation_long, 10)
```
