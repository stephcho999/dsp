[Think Stats Chapter 4 Exercise 2](http://greenteapress.com/thinkstats2/html/thinkstats2005.html#toc41) (a random distribution)

## The Problem
Generate 1000 random numbers between 0 and 1 using the method `np.random.random`.
Determine whether the distribution is uniform by plotting the PMF & CDF, 
that is whether each value has equal probability to be generated.

## The Solution
After generating 1000 random numbers using the above method, using the thinkstats2
methods `.Pmf()` and `.Cdf()`, the PMF and CDF were generated. They were then plotted
using `thinkplot` methods. <p>
Upon plotting the two distributions, it was clear that the distribution was uniform,
as the PMF showed that any particular value had a probability of 0.001 of being generated,
which corresponds with the fact that there were 1000 numbers generated, or a 1 in 1000 chance
for any particular value to be generated. <p>
Furthermore, the CDF was linear and approximately had a slope of 1, meaning that 
the probability of a number smaller than a specific value being generated is simply 
equal to the specific value itself. <p>
Therefore, we can see the distribution is uniform.

## The Code

    import numpy as np
    import thinkstats2
    import thinkplot
    
    # generate random sample
    sample = np.random.random(1000)
    
    # generate pmf
    pmf = thinkstats2.Pmf(sample, label='random')
    thinkplot.Pmf(pmf)
    thinkplot.Show(xlabel = 'number', ylabel='probability', ylim = [0,0.002])
    
    # generate cdf
    cdf = thinkstats2.Cdf(sample, label='random')
    thinkplot.Cdf(cdf)
    thinkplot.Show(xlabel='number', ylabel='cumulative probability')
