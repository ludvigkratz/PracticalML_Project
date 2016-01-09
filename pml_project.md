# Practical Machine Learing: Course Project

##Initial Data Analysis


```r
training <- read.csv('pml-training.csv')
#training <- training[, -1] #X Seems to be index
sapply(training, class)
summary(training$classe)
summary(training$user_name)
```

Since the testing set consist of 1 row per classe, I predict on a row-by-rwo basis.

Let us find which features to use.

First we find the percentage the missing values in each column. We remove the columns with a lot of NAs.

```r
percentage_na <- sapply(training, function(x) {sum(is.na(x)) / length(x)})
large_na <- percentage_na[percentage_na > 0.5]
dim(training)
```

```
## [1] 19622   160
```

```r
training <- training[, !(percentage_na > 0.5)]
dim(training)
```

```
## [1] 19622    93
```

Let us look at variance. We remove the features with near zero varinace. Since we look at each row independtly, the time should not affect the classe and we remove those features. The same applies to user_name and row index.

```r
library(caret)
nsv <- nearZeroVar(training, saveMetrics = TRUE)
training <- training[, !nsv$nzv]
training <- training[, -c(1:5)]
dim(training)
```

```
## [1] 19622    54
```

```r
col_names <- names(training)
```

##Pre Processing

Center and scale the data.

```r
preObj <- preProcess(training[,-54], method = c("center", "scale"))
training_norm <- predict(preObj, training[,-54])
training_norm <- data.frame(training_norm, classe = training$classe)
#sapply(training_norm, mean)
#sapply(training_norm, sd)
```


Train the model using lda.

```r
model <- train(classe ~ ., data = training_norm, method = "rf")
```

```
## Loading required package: randomForest
## randomForest 4.6-10
## Type rfNews() to see new features/changes/bug fixes.
```

```r
print('Run again')
```

```
## [1] "Run again"
```

```r
pred_train <- predict(model, training_norm)
confusionMatrix(pred_train, training_norm$classe)
```

```
## Confusion Matrix and Statistics
## 
##           Reference
## Prediction    A    B    C    D    E
##          A 5580    0    0    0    0
##          B    0 3797    0    0    0
##          C    0    0 3422    0    0
##          D    0    0    0 3216    0
##          E    0    0    0    0 3607
## 
## Overall Statistics
##                                      
##                Accuracy : 1          
##                  95% CI : (0.9998, 1)
##     No Information Rate : 0.2844     
##     P-Value [Acc > NIR] : < 2.2e-16  
##                                      
##                   Kappa : 1          
##  Mcnemar's Test P-Value : NA         
## 
## Statistics by Class:
## 
##                      Class: A Class: B Class: C Class: D Class: E
## Sensitivity            1.0000   1.0000   1.0000   1.0000   1.0000
## Specificity            1.0000   1.0000   1.0000   1.0000   1.0000
## Pos Pred Value         1.0000   1.0000   1.0000   1.0000   1.0000
## Neg Pred Value         1.0000   1.0000   1.0000   1.0000   1.0000
## Prevalence             0.2844   0.1935   0.1744   0.1639   0.1838
## Detection Rate         0.2844   0.1935   0.1744   0.1639   0.1838
## Detection Prevalence   0.2844   0.1935   0.1744   0.1639   0.1838
## Balanced Accuracy      1.0000   1.0000   1.0000   1.0000   1.0000
```

Predict on testing data. First load and preprocess the test data.

```r
testing <- read.csv('pml-testing.csv')
testing <- testing[, which(names(testing) %in% names(training))]
testing_norm <- predict(preObj, testing)
```


```r
pred_test <- predict(model, testing_norm)
print(pred_test)
```

```
##  [1] B A B A A E D B A A B C B A E E A B B B
## Levels: A B C D E
```



