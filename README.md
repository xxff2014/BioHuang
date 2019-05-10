# Huang-Baoquan
these are  my learning practices
--------------------- 
```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

# 1.相关系数矩阵及绘图

```{r message=FALSE}
rm(list = ls())
small.mtcars <- subset(mtcars,select = 1:10)
pairs(small.mtcars) #绘制变量间散点图
```


```{r message=FALSE}
library(arm)
library(corrplot)#加载需要的包
```

```{r}
sm.cor <- cor(small.mtcars)
arm::corrplot(sm.cor,color = T)#绘制相关系数矩阵
```

```{r}
par(mfrow=c(1,1))
corrplot::corrplot(sm.cor,type = "upper")#绘制相关系数矩阵
```

# 2.数据格式转换（长格式，宽格式，列联表）
```{r message=FALSE}
library(reshape2)
str(airquality) #看看数据长啥样
mydat <- na.omit(airquality) #去掉缺失值
head(mydat)
names(mydat) <- tolower(names(mydat))
mytable <- melt(mydat,id.vars = c("month","day"),variable.name = "airquality")#转化为长格式
dcast.data <- dcast(mytable,month~airquality,fun.aggregate = mean)#重铸，以下方法为异曲同工
agg.data <- aggregate(mytable[,4],list(month=mytable$month,airquality=mytable$airquality),FUN=mean)
agg.tab.data <- xtabs(data=agg.data,x~ month+airquality)
dcast.data;agg.tab.data #比较下
```
