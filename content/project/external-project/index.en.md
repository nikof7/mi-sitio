---
title: "Hello R Markdown"
author: "Frida Gomam"
date: 2020-12-01T21:13:14-05:00
categories: ["R"]
tags: ["R Markdown", "plot", "regression"]
---



# R Markdown

This is an R Markdown doasdcument. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.
 
Yoasdsadasdasdasdas asdf asdfasd fsd

```r
summary(cars)
##      speed           dist       
##  Min.   : 4.0   Min.   :  2.00  
##  1st Qu.:12.0   1st Qu.: 26.00  
##  Median :15.0   Median : 36.00  
##  Mean   :15.4   Mean   : 42.98  
##  3rd Qu.:19.0   3rd Qu.: 56.00  
##  Max.   :25.0   Max.   :120.00
fit <- lm(dist ~ speed, data = cars)
fit
## 
## Call:
## lm(formula = dist ~ speed, data = cars)
## 
## Coefficients:
## (Intercept)        speed  
##     -17.579        3.932
```

# Including Plots

You can also embed plots. See Figure <a href="#fig:pie">1</a> for example:


```r
plot(x = cars$speed, y = cars$dist)
```

<div class="figure">
<img src="{{< blogdown/postref >}}index.en_files/figure-html/pie-1.png" alt="A fancy pie chart." width="672" />
<p class="caption">Figure 1: A fancy pie chart.</p>
</div>
