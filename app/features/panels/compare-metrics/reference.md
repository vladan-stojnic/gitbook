# Reference

## X-Axis

![Selecting X-Axis](../../../../.gitbook/assets/image%20%2815%29.png)

You can set the X-Axis of a line plot to any value that you have logged with wandb.log as long as it's always logged as a number.

## Y-Axis Variables

You can set the y-axis variables to any value you have logged with wandb.log as long as you were logging numbers, arrays of numbers or a histogram of numbers. If you logged more than 1500 points for a variable, wandb samples down to 1500 points.

{% hint style="info" %}
You can change the color of your y axis lines by changing the color of the run in the runs table.
{% endhint %}

## X Range and Y Range

You can change the maximum and minimum values of X and Y for the plot.

X range default is from the smallest value of your x-axis to the largest.

Y range default is from the smallest value of your metrics and zero to the largest value of your metrics.

## Max Runs/Groups

By default you will only plot 10 runs or groups of runs. The runs will be taken from the top of your runs table or run set, so if you sort your runs table or run set you can change the runs that are shown.

## Legend

You can control the legend of your chart to show for any run any config value that you logged and meta data from the runs such as the created at time or the user who created the run.

Example:

${config:x} will insert the config value of x for a run or group.

You can set \[\[$x: $y\]\] to display point specific values in the crosshair

## Grouping

You can aggregate all of the runs by turning on grouping, or group over an individual variable. You can also turn on grouping by grouping inside the table and the groups will automatically populate into the graph.

## Smoothing

You can set the [smoothing coefficient](../../../../library/technical-faq.md#what-formula-do-you-use-for-your-smoothing-algorithm) to be between 0 and 1 where 0 is no smoothing and 1 is maximum smoothing.

## Ignore Outliers

Ignore outliers makes the graph set the yaxis min and max to the 5th and 95th percentile of the data instead of setting it to make all data visible.

## Expression

Expression lets you plot values derived from metrics like 1-accuracy. It currently only works if you are plotting a single metric. You can do simple arithmetic expressions, +, -, \*, / and % as well as \*\* for powers.

## Plot style

Select a style for your line plot.

**Line plot:**

![](../../../../.gitbook/assets/image%20%285%29%20%282%29.png)

**Area plot:**

![](../../../../.gitbook/assets/image%20%2835%29%20%281%29%20%282%29%20%281%29.png)

**Percentage area plot:**

![](../../../../.gitbook/assets/image%20%2869%29%20%284%29%20%286%29%20%282%29.png)

