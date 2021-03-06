---
title       : Developing Data Products
subtitle    : Course Project 
author      : gsk - September 2014
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [mathjax]     # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Introduction

### Objective
The goal of this document is to briefly describe a web application that allows users to easily assess their current weight in relation to a recognized international standard.

### Weight and Health
BMI is a useful measure of overweight and obesity. It is calculated from the individual's height and weight. BMI is an estimate of body fat and a good gauge of the individual's risk for diseases that can occur with more body fat. The higher the BMI, the higher your risk for certain diseases such as heart disease, high blood pressure, type 2 diabetes, gallstones, breathing problems, and certain cancers. [National Institute of Health](http://www.nhlbi.nih.gov/health/educational/lose_wt/risk.htm)

### Application
Weight Controller is a web application that allows users to compute two indices (BMI and BMI Prime) and to visualize their current BMI position according to well-established health standards.

---

## Application description

Both inputs, weight and height, can be entered using Metric or Imperial units. BMI and BMI Prime are computed. Values of BMI Prime above 1.00 implies the person is overweighted.


![Weight Controller](./assets/img/bmi_60.PNG)

The graph represents the position of the individual's BMI relative to the lower and upper healthy limits. The zone to the left of the green line corresponds to underweight values, while that to the right of the red line to overweight ones.

---

## BMI computation



BMI is computed using the following code. The function unit.conv() takes care of the input variables' units, returning weight and height in kg and cm.


```r
bmiCalc <- function(weight, height, units) {
    # computes BMI in kg/m2
    wh <- unit.conv(weight, height, units)
    return((wh[1] / wh[2]^2) * 10000)
}
```

Different input variable's unit systems are accepted. For example, if the user entered weight in Lb and height in cm, the function would be called as below. Note that BMI is always returned in \(Kg/m^2\), its standard units.


```r
bmiCalc(176, 180, c(2,1))
```

[1] 24.64

--- 

## Installation and Use

The application can be accessed online on [RStudio's Shinyapp Server](https://guye.shinyapps.io/BMICalc/) (recommended) or it can be downloaded from github and run on the user's computer. 

To download Weight Controller from github please follow [this link](https://github.com/GuySK/DDP). 

##### Files to download

    1. ui.R
    2. server.R

##### Running the App

Create a new directory named 'bmi' and place both files there. Then enter the following lines on your R console.


```r
1. setwd("/your_path_to_bmi/bmi/..")    # position yourself on bmi's parent directory
2. library(shiny)                       # load Shiny
3. runApp("bmi", launch.browser=1)      # run application on default browser
```
