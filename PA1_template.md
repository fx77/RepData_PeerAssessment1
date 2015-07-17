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

```r
interval_mean <- tapply(activity$steps, activity$interval, mean, na.rm=TRUE)
intervals<- strptime(sprintf("%04d", as.numeric(names(interval_mean))), format="%H%M")
plot(intervals, interval_mean, type="l")
```

![](PA1_template_files/figure-html/unnamed-chunk-5-1.png) 

Interval with maximum number of averaged steps:

```r
m <- max(interval_mean)
ind <- which(interval_mean==m)
names(interval_mean[ind])
```

```
## [1] "835"
```


## Imputing missing values
The number of missing values (NA) is:

```r
length(which(is.na(activity$steps)))
```

```
## [1] 2304
```
Replacing missing values with an average for all intervals and creating a new dataset:

```r
activity2 <- activity
activity2$steps[is.na(activity2$steps)] <- mean(activity2$steps, na.rm=TRUE)
```
Making a histogram of the new daily total number of steps:

```r
daily_total2 <- tapply(activity2$steps, activity2$date, sum, na.rm=TRUE)
DF2 <- data.frame(date=names(daily_total2), sum=daily_total2)
hist(DF2$sum)
```

![](PA1_template_files/figure-html/unnamed-chunk-9-1.png) 

The mean of the new total number of steps per day:

```r
mean(DF2$sum)
```

```
## [1] 10766.19
```

The median of new the total number of steps per day:

```r
median(DF2$sum)
```

```
## [1] 10766.19
```

Both mean and median number of steps per day increased. 

## Are there differences in activity patterns between weekdays and weekends?
