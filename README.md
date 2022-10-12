## Q1. “Q_” 로 시작하는 변수는 범주형(factor)으로, 나머지 변수는 숫자형(integer)으로 만드세요.   

```
library(data.table);library(magrittr);library(ggpubr);library(rvg);library(officer) 
a <- fread("https://raw.githubusercontent.com/jinseob2kim/R-skku-biohrs/main/data/example_g1e.csv")

var.factor <- grep("Q_", names(a), value = T)  
var.conti <- names(a)[!(names(a) %in% var.factor)] 

a[, (var.factor) := lapply(.SD, as.factor), .SD = var.factor]
a[, (var.conti) := lapply(.SD, as.numeric), .SD = var.conti]
sapply(a, class)
```
![q1](q1.png)

## Q2. 연속 변수 “WSTC”와 “BMI”의 연도별 평균 및 표준편차를 구하세요.

```
both <- aggregate(cbind(WSTC, BMI) ~ EXMD_BZ_YYYY, data = a, function(x){c(mean = mean(x), sd = sd(x))})
aggregate(cbind(WSTC, BMI) ~ EXMD_BZ_YYYY, data = a, function(x){c(mean = mean(x), sd = sd(x))})
```
