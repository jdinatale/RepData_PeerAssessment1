# Reproducible Research: Peer Assessment 1

## Loading and preprocessing the data

First, unzip the data file and read it into R. Add a new column which converts the interval from military time to minutes since midnight.


```r
unzip("activity.zip")
activity <- read.csv("activity.csv", colClasses = c("integer", "Date", "integer"))
activity$intervalminutes <- activity$interval %/% 100 * 60 + activity$interval %% 100
```

## What is mean total number of steps taken per day?

Calculate total steps per day, plot a histogram and report mean and median


```r
dailysteps <- aggregate(steps~date, data = activity, FUN = "sum")
hist(dailysteps$steps, main = "Histogram of Total Steps per Day", xlab = "Total Steps per Day")
```

![plot of chunk hist](figure/hist.png) 

Mean steps per day:

```r
mean(dailysteps$steps)
```

```
## [1] 10766
```

Median steps per day:

```r
median(dailysteps$steps)
```

```
## [1] 10765
```

## What is the average daily activity pattern?

Calculate average for each interval, plot daily activity pattern and report interval with maximum number of steps.
Note: Plot uses minutes past midnight instead of original intervals (military time) in order to prevent "jumps" at the hour boundaries.


```r
avgsteps <- aggregate(steps~intervalminutes + interval, data = activity, FUN = "mean")
plot(avgsteps$intervalminutes, avgsteps$steps, type = "l", main = "Average Daily Activity", xlab = "Minutes", 
     ylab = "Average Number of Steps")
```

![plot of chunk daily](figure/daily.png) 

Interval with maximum number of steps:


```r
avgsteps[which.max(avgsteps$steps),]
```

```
##     intervalminutes interval steps
## 104             515      835 206.2
```

## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
