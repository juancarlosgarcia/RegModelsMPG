Transmission Effects On MPG In Cars
====================================

# Executive Summary
In this paper, we look at 1974 Motor Trend Data [1] for the purpose of evaluating factors on fuel efficiency. We specifically are interested in the
effects of automatic vs manual transmission on the gas mileage. Our analysis predicted that the weight of the car directly related, and the choice of manual or automatic depends on it.

# Data
The data frame consists of 32 observations on 11 variables.
- mpg: Miles/(US) gallon
- cyl: Number of cylinders
- disp: Displacement (cu.in.)
- hp: Gross horsepower
- drat: Rear axle ratio
- wt: Weight (lb/1000)
- qsec: 1/4 mile time
- vs: V/S
- am: Transmission (0 = automatic, 1 = manual)
- gear: Number of forward gears


```r
data(mtcars)
mtcarst <- within(mtcars, {
    am <- factor(am, labels = c("Automatic", "Manual"))
    vs <- factor(vs, labels = c("Vengine", "Iengine"))
})
head(mtcarst)
```

```
##                    mpg cyl disp  hp drat    wt  qsec      vs        am
## Mazda RX4         21.0   6  160 110 3.90 2.620 16.46 Vengine    Manual
## Mazda RX4 Wag     21.0   6  160 110 3.90 2.875 17.02 Vengine    Manual
## Datsun 710        22.8   4  108  93 3.85 2.320 18.61 Iengine    Manual
## Hornet 4 Drive    21.4   6  258 110 3.08 3.215 19.44 Iengine Automatic
## Hornet Sportabout 18.7   8  360 175 3.15 3.440 17.02 Vengine Automatic
## Valiant           18.1   6  225 105 2.76 3.460 20.22 Iengine Automatic
##                   gear carb
## Mazda RX4            4    4
## Mazda RX4 Wag        4    4
## Datsun 710           4    1
## Hornet 4 Drive       3    1
## Hornet Sportabout    3    2
## Valiant              3    1
```


# Exploratory Data Analysis
The initial exploration of the data use a boxplot in the [Appendix](#boxplot) shows a comparison miles per gallon (MPG) versus transmission (0 = Automatic, 1 = Manual). This plot motivates us to build a linear regression for MPG over transmission.

The pairs scatterplots in the [Appendix](#scatter) allows to observe that MPG appeared to be highly correlated with all the variables
except rear axle ratio and transmission.

#Models
We need to check that a relationship does exist between MPG and Transmission with a simple linear model.


```r
model1 <- lm(mpg ~ am, mtcarst)
summary(model1)$coefficients
```

```
##             Estimate Std. Error t value  Pr(>|t|)
## (Intercept)   17.147      1.125  15.247 1.134e-15
## amManual       7.245      1.764   4.106 2.850e-04
```

```r
summary(model1)
```

```
## 
## Call:
## lm(formula = mpg ~ am, data = mtcarst)
## 
## Residuals:
##    Min     1Q Median     3Q    Max 
## -9.392 -3.092 -0.297  3.244  9.508 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept)    17.15       1.12   15.25  1.1e-15 ***
## amManual        7.24       1.76    4.11  0.00029 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 4.9 on 30 degrees of freedom
## Multiple R-squared:  0.36,	Adjusted R-squared:  0.338 
## F-statistic: 16.9 on 1 and 30 DF,  p-value: 0.000285
```

We can see a string relationship does exist with a p-value 

# Appendix

## MPG versus Transmission

```r
op <- par(mar = c(2, 2, 1, 1))
boxplot(mpg ~ am, data = mtcarst)
stripchart(mpg ~ am, data = mtcarst, vertical = T, method = "jitter", pch = 20, 
    add = T)
```

![plot of chunk boxplot](figure/boxplot.png) 

```r
par(op)
```

## MPG against all variables

```r
require(graphics)
pairs(mtcarst[, c(1:6, 9)], panel = panel.smooth)
```

![plot of chunk scatter](figure/scatter.png) 



