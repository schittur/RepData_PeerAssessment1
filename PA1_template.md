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
meanstepsperday <- aggregate(steps ~ date, data=activitydata, FUN=mean);
ggplot(meanstepsperday, aes(x=date, y=steps)) +
    xlab("Date") + ylab("Total Steps") + 
    geom_bar(stat="identity") +
    scale_x_date(labels = date_format("%m-%d-%Y")) +
    ggtitle("Total Steps by Date") +
    theme(plot.title = element_text(lineheight=.8, face="bold"));
```

![](PA1_template_files/figure-html/unnamed-chunk-2-1.png) 


## What is the average daily activity pattern?



## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?

