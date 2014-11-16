# Reproducible Research: Peer Assessment 1

## Loading and preprocessing the data

```r
require(ggplot2);
```

```
## Loading required package: ggplot2
```

```r
require(scales);
```

```
## Loading required package: scales
```

```r
setwd("C:\\Coursera\\assignment");
activitydata <- read.csv("activity.csv");
activitydata$date = as.Date(activitydata$date, format="%Y-%M-%d")
```

## What is mean total number of steps taken per day?


```r
totalstepsperday <- aggregate(steps ~ date, data=activitydata, FUN=sum);

meansteps = mean(totalstepsperday$steps);
mediansteps = median(totalstepsperday$steps);

ggplot(totalstepsperday, aes(x=date, y=steps)) +
    xlab("Date") + ylab("Total Steps") + 
    geom_bar(stat="identity") +
    scale_x_date(labels = date_format("%m-%d-%Y")) +
    ggtitle("Total Steps by Date") +
    theme(plot.title = element_text(lineheight=.8, face="bold"));
```

![](PA1_template_files/figure-html/unnamed-chunk-2-1.png) 

Mean total steps per day = 1.9144621\times 10^{4}

Median total steps per day = 20670

## What is the average daily activity pattern?

```r
averagestepsperinterval <- aggregate(steps ~ interval, data=activitydata, FUN=mean);
plot(averagestepsperinterval$steps ~ averagestepsperinterval$interval, type="l",
      xlab= "Interval", ylab = "Average Steps")
title(main="Average Steps per Interval");
```

![](PA1_template_files/figure-html/unnamed-chunk-3-1.png) 

```r
maxinterval = 
averagestepsperinterval[which (
averagestepsperinterval$steps == max(averagestepsperinterval$steps)),]$interval
```
5 Minute interval having max average steps = 835




## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?

