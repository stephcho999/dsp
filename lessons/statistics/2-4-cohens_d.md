[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

## The Problem
Using variable `birthwgt_lb`, find out whether first-born babies are lighter or heavier than others. <br>
Compute Cohen's d to quantify the difference.

## The Solution
First, I read in the respondent data to variable `preg`. 
Then, I sorted out stillborn cases using the `outcome` column.
Using the values in the `birthord` column, I was able to sort the live births based on whether 
the children were firstborn or not. <br>
At this point, I selected the `birthwgt_lb` column for each group (firstborn vs others)
to be used for comparison.
I determined the difference in the mean between the two groups, then wrote my own 
function for computing Cohen's d (by using basic pandas methods such as `.mean()`, `.var()`, `.count()`).
<p></p>
The resulting Cohen's d computed from birth weight data (.108) is much larger than the 
Cohen's d computed from pregnancy length data (.029), meaning the significance of the difference
is much more noteworthy in the birth weight data.

## The Code
    import nsfg
    import math
    preg = nsfg.ReadFemPreg()
    
    live = preg[preg['outcome'] == 1]
    first_live = live[live['birthord'] == 1]
    other_live = live[live['birthord'] != 1]
    
    first_wgt = first_live['birthwgt_lb']
    other_wgt = other_live['birthwgt_lb']
    
    
    def cohen_d(series1, series2):
        """
        Computes Cohen's d for the two given iterable objects
        series1, series2: iterable objects
        """
        mean1 = series1.mean()
        mean2 = series2.mean()
        var1 = series1.var()
        var2 = series2.var()
        count1 = series1.count()
        count2 = series2.count()
    
        pooled_var = ((var1 * count1) + (var2 * count2)) / (count1 + count2)
        pooled_std = math.sqrt(pooled_var)
    
        diff = mean1 - mean2
    
        cohen_d = diff / pooled_std
    
        return cohen_d
    
    print(cohen_d(first_wgt, other_wgt))

