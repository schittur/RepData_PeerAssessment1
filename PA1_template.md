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
strmediansteps = sprintf("%10.2f", mediansteps);

ggplot(totalstepsperday, aes(x=date, y=steps)) +
    xlab("Date") + ylab("Total Steps") + 
    geom_bar(stat="identity") +
    scale_x_date(labels = date_format("%m-%d-%Y")) +
    ggtitle("Total Steps by Date") +
    theme(plot.title = element_text(lineheight=.8, face="bold"));
```

![](PA1_template_files/figure-html/unnamed-chunk-2-1.png) 

Mean total steps per day = 1.9144621\times 10^{4}

Median total steps per day =   20670.00

## What is the average daily activity pattern?



## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?

