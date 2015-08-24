SimulationCraft works according to [Law of large numbers](http://en.wikipedia.org/wiki/Law_of_large_numbers), which claims the following:

```
The average of the results obtained from a large number of trials should be close to the expected value,
and will tend to become closer as more trials are performed.
```


So if we set iterations=infinity, SimulationCraft will yield a precise result that will be perfect in comparison with theorycraft - no assumptions, pure modelling, but definitive output.

However, this is impossible and full raid sims take quite a significant amount of time even with few iterations. Thus we have to deal with variance in our results, that's especially noticeable when we calculate scaling, i.e. small differences between two dps.

To know how close the sample mean is to the expected value, we can use the [Central limit theorem](http://en.wikipedia.org/wiki/Central_limit_theorem), which claims the following:

```
Let X1, X2, X3, ... Xn be a sequence of n independent and identically distributed random variables
having each finite values of expectation µ and variance σ^2 > 0. Then the distribution of the sample
average of these random variables approaches a normal distribution with mean µ and variance σ^2 / n
irrespective of the shape of the original distribution.
```
> ![http://upload.wikimedia.org/wikipedia/en/f/f3/Central_limit_thm.png](http://upload.wikimedia.org/wikipedia/en/f/f3/Central_limit_thm.png)


Using this information and combining it with a [Confidence interval](http://en.wikipedia.org/wiki/Confidence_(statistics)), we can now make the following statements about the variation of the mean dps:

  * 95% of the time the same simulation is run, the true(population) mean dps will be be within the confidence interal, which is +-1.96 `*` σ / sqrt( n ) of the mean dps.

> In other words: If you run the exact same simulation N times, you'd expect N `*` 0.95 of the simulations to capture the true mean dps within their respective 95% confidence interval.

  * The same can be said about the DPS difference lying 95% of the time within 1.96 `*` sqrt( 1.96 ) `*` σ / sqrt( n ) neighbourhood of difference between two average DPS values, given the same mean variation (useful for scaling simulations and spec comparisons).

To make practical use of this, we add some final assumption:

- We replace the population standard deviation by the standard deviation of the sample.


---


SimulationCraft also reports a series of statistical metrics, e.g. stddev, min and max, range, 10th and 90th percentile and #iterations needed for specific error thresholds.

As of [r9633](https://code.google.com/p/SimulationCraft/source/detail?r=9633) it is possible to specify a custom confidence level, whereas the default remains 95%.


---


![http://1.chart.apis.google.com/chart?chs=525x185&cht=lc&chg=20,20&chco=FF0000&chxr=0,33185,33346|2,0,0.0398&chf=bg,s,333333&chxt=x,x,y,y&chxl=1:|DPS|3:|p&chtt=60.00%25+Confidence+Interval&chxs=0,ffffff|1,ffffff|2,ffffff|3,ffffff&chts=dddddd,18&chfd=0,x,33185,33346,0.04982692,100*exp(-(x-33265)^2/(2*20^2))&chd=t:-1&chm=B,C6D9FD,0,1272:1950,0&name=60confidence.jpg](http://1.chart.apis.google.com/chart?chs=525x185&cht=lc&chg=20,20&chco=FF0000&chxr=0,33185,33346|2,0,0.0398&chf=bg,s,333333&chxt=x,x,y,y&chxl=1:|DPS|3:|p&chtt=60.00%25+Confidence+Interval&chxs=0,ffffff|1,ffffff|2,ffffff|3,ffffff&chts=dddddd,18&chfd=0,x,33185,33346,0.04982692,100*exp(-(x-33265)^2/(2*20^2))&chd=t:-1&chm=B,C6D9FD,0,1272:1950,0&name=60confidence.jpg)

![http://2.chart.apis.google.com/chart?chs=525x185&cht=lc&chg=20,20&chco=FF0000&chxr=0,33180,33341|2,0,0.0397&chf=bg,s,333333&chxt=x,x,y,y&chxl=1:|DPS|3:|p&chtt=97.00%25+Confidence+Interval&chxs=0,ffffff|1,ffffff|2,ffffff|3,ffffff&chts=dddddd,18&chfd=0,x,33180,33341,0.04974335,100*exp(-(x-33261)^2/(2*20^2))&chd=t:-1&chm=B,C6D9FD,0,740:2493,0&name=97confidence.jpg](http://2.chart.apis.google.com/chart?chs=525x185&cht=lc&chg=20,20&chco=FF0000&chxr=0,33180,33341|2,0,0.0397&chf=bg,s,333333&chxt=x,x,y,y&chxl=1:|DPS|3:|p&chtt=97.00%25+Confidence+Interval&chxs=0,ffffff|1,ffffff|2,ffffff|3,ffffff&chts=dddddd,18&chfd=0,x,33180,33341,0.04974335,100*exp(-(x-33261)^2/(2*20^2))&chd=t:-1&chm=B,C6D9FD,0,740:2493,0&name=97confidence.jpg)