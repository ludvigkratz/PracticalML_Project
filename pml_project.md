# Practical Machine Learing: Course Project
Ludvig Kratz
2016-01-08
Coursera

##Initial Data Analysis

Load the training data and look at some values.


```r
training <- read.csv('pml-training.csv')
#training <- training[, -1] #X Seems to be index
sapply(training, class)
```

```
##                        X                user_name     raw_timestamp_part_1 
##                "integer"                 "factor"                "integer" 
##     raw_timestamp_part_2           cvtd_timestamp               new_window 
##                "integer"                 "factor"                 "factor" 
##               num_window                roll_belt               pitch_belt 
##                "integer"                "numeric"                "numeric" 
##                 yaw_belt         total_accel_belt       kurtosis_roll_belt 
##                "numeric"                "integer"                 "factor" 
##      kurtosis_picth_belt        kurtosis_yaw_belt       skewness_roll_belt 
##                 "factor"                 "factor"                 "factor" 
##     skewness_roll_belt.1        skewness_yaw_belt            max_roll_belt 
##                 "factor"                 "factor"                "numeric" 
##           max_picth_belt             max_yaw_belt            min_roll_belt 
##                "integer"                 "factor"                "numeric" 
##           min_pitch_belt             min_yaw_belt      amplitude_roll_belt 
##                "integer"                 "factor"                "numeric" 
##     amplitude_pitch_belt       amplitude_yaw_belt     var_total_accel_belt 
##                "integer"                 "factor"                "numeric" 
##            avg_roll_belt         stddev_roll_belt            var_roll_belt 
##                "numeric"                "numeric"                "numeric" 
##           avg_pitch_belt        stddev_pitch_belt           var_pitch_belt 
##                "numeric"                "numeric"                "numeric" 
##             avg_yaw_belt          stddev_yaw_belt             var_yaw_belt 
##                "numeric"                "numeric"                "numeric" 
##             gyros_belt_x             gyros_belt_y             gyros_belt_z 
##                "numeric"                "numeric"                "numeric" 
##             accel_belt_x             accel_belt_y             accel_belt_z 
##                "integer"                "integer"                "integer" 
##            magnet_belt_x            magnet_belt_y            magnet_belt_z 
##                "integer"                "integer"                "integer" 
##                 roll_arm                pitch_arm                  yaw_arm 
##                "numeric"                "numeric"                "numeric" 
##          total_accel_arm            var_accel_arm             avg_roll_arm 
##                "integer"                "numeric"                "numeric" 
##          stddev_roll_arm             var_roll_arm            avg_pitch_arm 
##                "numeric"                "numeric"                "numeric" 
##         stddev_pitch_arm            var_pitch_arm              avg_yaw_arm 
##                "numeric"                "numeric"                "numeric" 
##           stddev_yaw_arm              var_yaw_arm              gyros_arm_x 
##                "numeric"                "numeric"                "numeric" 
##              gyros_arm_y              gyros_arm_z              accel_arm_x 
##                "numeric"                "numeric"                "integer" 
##              accel_arm_y              accel_arm_z             magnet_arm_x 
##                "integer"                "integer"                "integer" 
##             magnet_arm_y             magnet_arm_z        kurtosis_roll_arm 
##                "integer"                "integer"                 "factor" 
##       kurtosis_picth_arm         kurtosis_yaw_arm        skewness_roll_arm 
##                 "factor"                 "factor"                 "factor" 
##       skewness_pitch_arm         skewness_yaw_arm             max_roll_arm 
##                 "factor"                 "factor"                "numeric" 
##            max_picth_arm              max_yaw_arm             min_roll_arm 
##                "numeric"                "integer"                "numeric" 
##            min_pitch_arm              min_yaw_arm       amplitude_roll_arm 
##                "numeric"                "integer"                "numeric" 
##      amplitude_pitch_arm        amplitude_yaw_arm            roll_dumbbell 
##                "numeric"                "integer"                "numeric" 
##           pitch_dumbbell             yaw_dumbbell   kurtosis_roll_dumbbell 
##                "numeric"                "numeric"                 "factor" 
##  kurtosis_picth_dumbbell    kurtosis_yaw_dumbbell   skewness_roll_dumbbell 
##                 "factor"                 "factor"                 "factor" 
##  skewness_pitch_dumbbell    skewness_yaw_dumbbell        max_roll_dumbbell 
##                 "factor"                 "factor"                "numeric" 
##       max_picth_dumbbell         max_yaw_dumbbell        min_roll_dumbbell 
##                "numeric"                 "factor"                "numeric" 
##       min_pitch_dumbbell         min_yaw_dumbbell  amplitude_roll_dumbbell 
##                "numeric"                 "factor"                "numeric" 
## amplitude_pitch_dumbbell   amplitude_yaw_dumbbell     total_accel_dumbbell 
##                "numeric"                 "factor"                "integer" 
##       var_accel_dumbbell        avg_roll_dumbbell     stddev_roll_dumbbell 
##                "numeric"                "numeric"                "numeric" 
##        var_roll_dumbbell       avg_pitch_dumbbell    stddev_pitch_dumbbell 
##                "numeric"                "numeric"                "numeric" 
##       var_pitch_dumbbell         avg_yaw_dumbbell      stddev_yaw_dumbbell 
##                "numeric"                "numeric"                "numeric" 
##         var_yaw_dumbbell         gyros_dumbbell_x         gyros_dumbbell_y 
##                "numeric"                "numeric"                "numeric" 
##         gyros_dumbbell_z         accel_dumbbell_x         accel_dumbbell_y 
##                "numeric"                "integer"                "integer" 
##         accel_dumbbell_z        magnet_dumbbell_x        magnet_dumbbell_y 
##                "integer"                "integer"                "integer" 
##        magnet_dumbbell_z             roll_forearm            pitch_forearm 
##                "numeric"                "numeric"                "numeric" 
##              yaw_forearm    kurtosis_roll_forearm   kurtosis_picth_forearm 
##                "numeric"                 "factor"                 "factor" 
##     kurtosis_yaw_forearm    skewness_roll_forearm   skewness_pitch_forearm 
##                 "factor"                 "factor"                 "factor" 
##     skewness_yaw_forearm         max_roll_forearm        max_picth_forearm 
##                 "factor"                "numeric"                "numeric" 
##          max_yaw_forearm         min_roll_forearm        min_pitch_forearm 
##                 "factor"                "numeric"                "numeric" 
##          min_yaw_forearm   amplitude_roll_forearm  amplitude_pitch_forearm 
##                 "factor"                "numeric"                "numeric" 
##    amplitude_yaw_forearm      total_accel_forearm        var_accel_forearm 
##                 "factor"                "integer"                "numeric" 
##         avg_roll_forearm      stddev_roll_forearm         var_roll_forearm 
##                "numeric"                "numeric"                "numeric" 
##        avg_pitch_forearm     stddev_pitch_forearm        var_pitch_forearm 
##                "numeric"                "numeric"                "numeric" 
##          avg_yaw_forearm       stddev_yaw_forearm          var_yaw_forearm 
##                "numeric"                "numeric"                "numeric" 
##          gyros_forearm_x          gyros_forearm_y          gyros_forearm_z 
##                "numeric"                "numeric"                "numeric" 
##          accel_forearm_x          accel_forearm_y          accel_forearm_z 
##                "integer"                "integer"                "integer" 
##         magnet_forearm_x         magnet_forearm_y         magnet_forearm_z 
##                "integer"                "numeric"                "numeric" 
##                   classe 
##                 "factor"
```

```r
summary(training$classe)
```

```
##    A    B    C    D    E 
## 5580 3797 3422 3216 3607
```

```r
summary(training$user_name)
```

```
##   adelmo carlitos  charles   eurico   jeremy    pedro 
##     3892     3112     3536     3070     3402     2610
```

Since the testing set consist of 1 row per classe, I predict on a row-by-rwo basis.

Let us find which features to use.

##Pre Processing

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


Center and scale the data.

```r
preObj <- preProcess(training[,-54], method = c("center", "scale"))
training_norm <- predict(preObj, training[,-54])
training_norm <- data.frame(training_norm, classe = training$classe)
#sapply(training_norm, mean)
#sapply(training_norm, sd)
```

##Training

Train the model using random forest.

```r
set.seed(2)
model <- train(classe ~ ., data = training_norm, method = "rf")
```

```
## Loading required package: randomForest
## randomForest 4.6-10
## Type rfNews() to see new features/changes/bug fixes.
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

#Prediction

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

Random forest takes a long time to run but obtains 100 accuracy on both training and testing data.

