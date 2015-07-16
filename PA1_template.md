# Reproducible Research: Peer Assessment 1


## Loading and preprocessing the data
Data loaded from file "activity.csv".

```r
activity <- read.csv("activity.csv")
daily_total <- tapply(activity$steps, activity$date, sum, na.rm=TRUE)
DF <- data.frame(date=names(daily_total), sum=daily_total)
```


## What is mean total number of steps taken per day?
The histogram of the total number of steps per day:

```r
hist(DF$sum)
```

![](PA1_template_files/figure-html/unnamed-chunk-2-1.png) 

The mean of the total number of steps per day:

```r
mean(DF$sum)
```

```
## [1] 9354.23
```

The median of the total number of steps per day:

```r
median(DF$sum)
```

```
## [1] 10395
```

## What is the average daily activity pattern?



## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
