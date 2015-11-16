---
title       : Miles per Gallon (MPG) Estimation App
subtitle    : The Regression Equation Behind the MPG Estimation
author      : Ganesh Krishnamurthy
job         : Coursera student
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Introduction

When in the market to buy a car, one of the important economical considerations is the miles per gallon (MPG) of the desired vehicle. There are a variety of vehicle configuration/properties that impact the MPG. Some of these factors are:

1. Automatic vs Manual Transmission
2. Horsepower
3. Weight
4. # of cylinders in the engine
5. # of carburetors
6. Accelaration, etc.

Multiple regression models were attempted on the "mtcars" datset and the best model was chosen to predict the MPG in the App.

--- .class #id 

## Exploring the mtcars Dataset


```r
data(mtcars);
head(mtcars);
```

```
##                    mpg cyl disp  hp drat    wt  qsec vs am gear carb
## Mazda RX4         21.0   6  160 110 3.90 2.620 16.46  0  1    4    4
## Mazda RX4 Wag     21.0   6  160 110 3.90 2.875 17.02  0  1    4    4
## Datsun 710        22.8   4  108  93 3.85 2.320 18.61  1  1    4    1
## Hornet 4 Drive    21.4   6  258 110 3.08 3.215 19.44  1  0    3    1
## Hornet Sportabout 18.7   8  360 175 3.15 3.440 17.02  0  0    3    2
## Valiant           18.1   6  225 105 2.76 3.460 20.22  1  0    3    1
```
The mtcars dataset containing 32 vehicles was used to develop a regression model to estimate the MPG given the various vehicle properties.

Predictors that did not intiutively fit with the vocabulary of a car-buyer were discarded. Because, requesting user inputs for such variables will just lead to confusion and bad inputs from the front end of the App. Example: Rear axle ratio (drat), number of carburetors (carb), and accelaration (qsec).

--- .class #id 

## Trying Multiple Prediction Models

Multiple linear models were attempted.

```r
fit1<-lm(data=mtcars, mpg ~ am);
fit2<-lm(data=mtcars, mpg ~ am + hp + am*hp);
fit3<-lm(data=mtcars, mpg ~ am + wt + am*wt);
fit4<-lm(data=mtcars, mpg ~ am + hp + wt + am*wt);
```
The best model was chosen and it came out to be fit4:

```r
anova(fit1, fit2, fit3, fit4);
```
The chosen model had the following cofficients for the properties of a car:

```r
fit4$coefficients;
```

```
## (Intercept)         am1          hp          wt      am1:wt 
## 30.94733319 11.55481296 -0.02694935 -2.51558550 -3.57790980
```

--- .class #id 

## Constructing the App with the Regression Equation of Best Fit

This formula was encapsulated into the server.R piece of the Shiny App. The front end (ui.R) collects the automatic vs manual transmission decision, the weight and the horsepower. This is passed to the server and the prediction is returned to the front end of the MPG APP.

Care is taken to show-back/confirm to the user the inputs they entered and the MPG prediction is shown. Enjoy this App at:
https://ganesh-krishnamurthy.shinyapps.io/Project




