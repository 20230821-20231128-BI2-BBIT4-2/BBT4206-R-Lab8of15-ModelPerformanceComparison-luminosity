Business Intelligence Project
================
<Specify your name here>
<Specify the date when you submitted the lab>

- [Business Intelligence Lab Submission
  Markdown](#business-intelligence-lab-submission-markdown)
- [Student Details](#student-details)
- [Setup Chunk](#setup-chunk)
- [Installing and Loading the Required Packages
  —-](#installing-and-loading-the-required-packages--)
  - [mlbench —-](#mlbench--)
  - [caret —-](#caret--)
  - [kernlab —-](#kernlab--)
  - [randomForest —-](#randomforest--)
- [Loading the Dataset —-iris](#loading-the-dataset--iris)
- [Resampling Function —-](#resampling-function--)
  - [Training the Models —-](#training-the-models--)
- [LDA](#lda)
- [CART](#cart)
- [KNN](#knn)
- [SVM](#svm)
- [Random Forest](#random-forest)
  - [LDA —-](#lda--)
  - [CART —-](#cart--)
  - [KNN —-](#knn--)
  - [SVM —-](#svm--)
  - [Random Forest —-](#random-forest--)
- [Showing the Results —-](#showing-the-results--)
  - [2. Box and Whisker Plot —-](#2-box-and-whisker-plot--)
- [This is useful for visually observing the spread of the estimated
  accuracies](#this-is-useful-for-visually-observing-the-spread-of-the-estimated-accuracies)
- [for different algorithms and how they
  relate.](#for-different-algorithms-and-how-they-relate)
  - [3. Dot Plots —-](#3-dot-plots--)
- [They show both the mean estimated accuracy as well as the 95%
  confidence](#they-show-both-the-mean-estimated-accuracy-as-well-as-the-95-confidence)
- [interval (e.g. the range in which 95% of observed scores
  fell).](#interval-eg-the-range-in-which-95-of-observed-scores-fell)
  - [4. Scatter Plot Matrix —-](#4-scatter-plot-matrix--)
- [This is useful when considering whether the predictions from
  two](#this-is-useful-when-considering-whether-the-predictions-from-two)
- [different algorithms are correlated. If weakly correlated, then they
  are
  good](#different-algorithms-are-correlated-if-weakly-correlated-then-they-are-good)
- [candidates for being combined in an ensemble
  prediction.](#candidates-for-being-combined-in-an-ensemble-prediction)
  - [5. Pairwise xyPlots —-](#5-pairwise-xyplots--)
- [You can zoom in on one pairwise comparison of the accuracy of
  trial-folds
  for](#you-can-zoom-in-on-one-pairwise-comparison-of-the-accuracy-of-trial-folds-for)
- [two models using an xyplot.](#two-models-using-an-xyplot)
- [or](#or)
  - [6. Statistical Significance Tests
    —-](#6-statistical-significance-tests--)
- [This is used to calculate the significance of the differences between
  the](#this-is-used-to-calculate-the-significance-of-the-differences-between-the)
- [metric distributions of the various
  models.](#metric-distributions-of-the-various-models)
  - [Upper Diagonal —-](#upper-diagonal--)
- [The upper diagonal of the table shows the estimated difference
  between
  the](#the-upper-diagonal-of-the-table-shows-the-estimated-difference-between-the)
- [distributions. If we think that LDA is the most accurate model from
  looking](#distributions-if-we-think-that-lda-is-the-most-accurate-model-from-looking)
- [at the previous graphs, we can get an estimate of how much better it
  is
  than](#at-the-previous-graphs-we-can-get-an-estimate-of-how-much-better-it-is-than)
- [specific other models in terms of absolute
  accuracy.](#specific-other-models-in-terms-of-absolute-accuracy)
  - [Lower Diagonal —-](#lower-diagonal--)
- [The lower diagonal contains p-values of the null
  hypothesis.](#the-lower-diagonal-contains-p-values-of-the-null-hypothesis)
- [The null hypothesis is a claim that “the models are the
  same”.](#the-null-hypothesis-is-a-claim-that-the-models-are-the-same)
- [A lower p-value is better (more
  significant).](#a-lower-p-value-is-better-more-significant)

# Business Intelligence Lab Submission Markdown

# Student Details

<table style="width:99%;">
<colgroup>
<col style="width: 43%" />
<col style="width: 38%" />
<col style="width: 17%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Student ID Numbers and Names of Group Members</strong></td>
<td><div class="line-block">1. 134982 - A - Austin Waswa</div>
<div class="line-block">2. 100230 - A - Richard Maana</div>
<div class="line-block">3. 134564 - A - Cynthia Omusundi</div></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td><strong>GitHub Classroom Group Name</strong></td>
<td>Luminosity</td>
</tr>
<tr class="odd">
<td><strong>Course Code</strong></td>
<td>BBT4206</td>
<td></td>
</tr>
<tr class="even">
<td><strong>Course Name</strong></td>
<td>Business Intelligence II</td>
<td></td>
</tr>
<tr class="odd">
<td><strong>Program</strong></td>
<td>Bachelor of Business Information Technology</td>
<td></td>
</tr>
<tr class="even">
<td><strong>Semester Duration</strong></td>
<td>21<sup>st</sup> August 2023 to 28<sup>th</sup> November 2023</td>
<td></td>
</tr>
</tbody>
</table>

# Setup Chunk

**Note:** the following “*KnitR*” options have been set as the defaults
in this markdown:  
`knitr::opts_chunk$set(echo = TRUE, warning = FALSE, eval = TRUE, collapse = FALSE, tidy.opts = list(width.cutoff = 80), tidy = TRUE)`.

More KnitR options are documented here
<https://bookdown.org/yihui/rmarkdown-cookbook/chunk-options.html> and
here <https://yihui.org/knitr/options/>.

``` r
knitr::opts_chunk$set(
    eval = TRUE,
    echo = TRUE,
    warning = FALSE,
    collapse = FALSE,
    tidy = TRUE
)
```

------------------------------------------------------------------------

**Note:** the following “*R Markdown*” options have been set as the
defaults in this markdown:

> output: github_document:  
> toc: yes  
> toc_depth: 4  
> fig_width: 6  
> fig_height: 4  
> df_print: default
>
> editor_options:  
> chunk_output_type: console

------------------------------------------------------------------------

**Note:** the following “*R Markdown*” options have been set as the
defaults:

# Installing and Loading the Required Packages —-

## mlbench —-

if (require(“mlbench”)) { require(“mlbench”) } else {
install.packages(“mlbench”, dependencies = TRUE, repos =
“<https://cloud.r-project.org>”) }

## caret —-

if (require(“caret”)) { require(“caret”) } else {
install.packages(“caret”, dependencies = TRUE, repos =
“<https://cloud.r-project.org>”) }

## kernlab —-

if (require(“kernlab”)) { require(“kernlab”) } else {
install.packages(“kernlab”, dependencies = TRUE, repos =
“<https://cloud.r-project.org>”) }

## randomForest —-

if (require(“randomForest”)) { require(“randomForest”) } else {
install.packages(“randomForest”, dependencies = TRUE, repos =
“<https://cloud.r-project.org>”) }

# Loading the Dataset —-iris

data(“iris”)

\#Data preprocessing 0 looking for missing values any_na(iris)

# Resampling Function —-

## Training the Models —-

\#the models are trianed with 10 fold repeated cross validation which
has 3 repeats

# LDA

# CART

# KNN

# SVM

# Random Forest

train_control \<- trainControl(method = “repeatedcv”, number = 10,
repeats = 3)

### LDA —-

set.seed(7) iris_model_lda \<- train(Species ~ ., data = iris, method =
“lda”, trControl = train_control)

### CART —-

set.seed(7) iris_model_cart \<- train(Species ~ ., data = iris, method =
“rpart”, trControl = train_control)

### KNN —-

set.seed(7) iris_model_knn \<- train(Species ~ ., data = iris, method =
“knn”, trControl = train_control)

### SVM —-

set.seed(7) iris_model_svm \<- train(Species ~ ., data = iris, method =
“svmRadial”, trControl = train_control)

### Random Forest —-

set.seed(7) iris_model_rf \<- train(Species ~ ., data = iris, method =
“rf”, trControl = train_control)

\##Calling the `resamples` Function —-

results \<- resamples(list(LDA = iris_model_lda, CART = iris_model_cart,
KNN = iris_model_knn, SVM = iris_model_svm, RF = iris_model_rf))

# Showing the Results —-

summary(results)

## 2. Box and Whisker Plot —-

# This is useful for visually observing the spread of the estimated accuracies

# for different algorithms and how they relate.

scales \<- list(x = list(relation = “free”), y = list(relation =
“free”)) bwplot(results, scales = scales)

## 3. Dot Plots —-

# They show both the mean estimated accuracy as well as the 95% confidence

# interval (e.g. the range in which 95% of observed scores fell).

scales \<- list(x = list(relation = “free”), y = list(relation =
“free”)) dotplot(results, scales = scales)

## 4. Scatter Plot Matrix —-

# This is useful when considering whether the predictions from two

# different algorithms are correlated. If weakly correlated, then they are good

# candidates for being combined in an ensemble prediction.

splom(results)

## 5. Pairwise xyPlots —-

# You can zoom in on one pairwise comparison of the accuracy of trial-folds for

# two models using an xyplot.

xyplot(results, models = c(“LDA”, “SVM”))

# or

xyplot(results, models = c(“SVM”, “CART”))

## 6. Statistical Significance Tests —-

# This is used to calculate the significance of the differences between the

# metric distributions of the various models.

### Upper Diagonal —-

# The upper diagonal of the table shows the estimated difference between the

# distributions. If we think that LDA is the most accurate model from looking

# at the previous graphs, we can get an estimate of how much better it is than

# specific other models in terms of absolute accuracy.

### Lower Diagonal —-

# The lower diagonal contains p-values of the null hypothesis.

# The null hypothesis is a claim that “the models are the same”.

# A lower p-value is better (more significant).

diffs \<- diff(results)

summary(diffs)
