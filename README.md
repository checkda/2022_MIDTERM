## Q1. “Q_” 로 시작하는 변수는 범주형(factor)으로, 나머지 변수는 숫자형(integer)으로 만드세요.   

```
library(data.table);library(magrittr);library(ggpubr);library(rvg);library(officer) 
a <- fread("https://raw.githubusercontent.com/jinseob2kim/R-skku-biohrs/main/data/example_g1e.csv")
```
```
var.factor <- grep("Q_", names(a), value = T)  
var.factor
```
  
```
var.conti <- names(a)[!(names(a) %in% var.factor)] 
var.conti
```
```
a[, (var.factor) := lapply(.SD, as.factor), .SD = var.factor]
a[, (var.conti) := lapply(.SD, as.numeric), .SD = var.conti]
sapply(a, class)
```
  EXMD_BZ_YYYY        RN_INDI     HME_YYYYMM   Q_PHX_DX_STK  Q_PHX_DX_HTDZ       
      "factor"      "numeric"      "numeric"      "integer"      "integer"     
  Q_PHX_DX_HTN    Q_PHX_DX_DM   Q_PHX_DX_DLD   Q_PHX_DX_PTB       Q_HBV_AG     
     "integer"      "integer"      "integer"      "integer"      "integer"     
      Q_SMK_YN Q_DRK_FRQ_V09N           HGHT           WGHT           WSTC     
     "integer"      "integer"      "numeric"      "numeric"      "numeric"     
           BMI          VA_LT          VA_RT         BP_SYS         BP_DIA    
     "numeric"      "numeric"      "numeric"      "numeric"      "numeric"    
      URN_PROT            HGB            FBS       TOT_CHOL             TG    
     "numeric"      "numeric"      "numeric"      "numeric"      "numeric"    
           HDL            LDL           CRTN           SGOT           SGPT    
     "numeric"      "numeric"      "numeric"      "numeric"      "numeric"     
           GGT            GFR     
     "numeric"      "numeric"    
