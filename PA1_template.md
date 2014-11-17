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

```r
missingvaluescount = sum(is.na(activitydata$steps));
```

Total Number of missing values in the dataset 2304

Filling missing values with the average steps over all intervals (keeping this simple because of lack of time)


```r
activitydata[which(is.na(activitydata$steps) == T), "steps"] <- 
  mean(activitydata$steps, na.rm=T);

totalstepsperday <- aggregate(steps ~ date, data=activitydata, FUN=sum);

meansteps_imput = mean(totalstepsperday$steps);
mediansteps_imput = median(totalstepsperday$steps);

ggplot(totalstepsperday, aes(x=date, y=steps)) +
    xlab("Date") + ylab("Total Steps") + 
    geom_bar(stat="identity") +
    scale_x_date(labels = date_format("%m-%d-%Y")) +
    ggtitle("Total Steps by Date (after Imputing)") +
    theme(plot.title = element_text(lineheight=.8, face="bold"));
```

![](PA1_template_files/figure-html/unnamed-chunk-5-1.png) 

```r
mean_diff <- meansteps_imput - meansteps;
median_diff <- mediansteps_imput - mediansteps;
```

Mean total steps per day (after imputing) = 1.9144621\times 10^{4}

Median total steps per day (after imputing) = 20670

### Differences after Imputing

Difference in mean after imput = 2232.8296248

Difference in median after imput = 1112

## Are there differences in activity patterns between weekdays and weekends?

Add a boolean column called "weekday" indicating if it is a weekday or not


```r
activitydata[, "weekday"] <- T;
activitydata[is.na(weekdays(activitydata$date)), "weekday"] <- F;
weekday_averagestepsperinterval <- 
    aggregate(steps ~ interval, data=activitydata[which(activitydata$weekday == T),], FUN=mean);
weekend_averagestepsperinterval <- 
    aggregate(steps ~ interval, data=activitydata[which(activitydata$weekday == F),], FUN=mean);

par(mfrow=c(2,1));

plot(weekday_averagestepsperinterval$steps ~ weekday_averagestepsperinterval$interval, type="l",
     xlab = "interval", ylab="steps")
title(main="WeekDay Average Steps per Interval", cex.main =0.8, col.main= "blue");

plot(weekend_averagestepsperinterval$steps ~ weekend_averagestepsperinterval$interval, type="l",
     xlab= "interval", ylab="steps")
title(main="WeekEnd Average Steps per Interval", cex.main =0.8, col.main="green");
```

![](PA1_template_files/figure-html/unnamed-chunk-6-1.png) 

Conclusion : from the above Weekend steps appear to be more for any interval.
