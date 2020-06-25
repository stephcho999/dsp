[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

## The Problem
Using the column `numkdhh`, construct the actual distribution of children per household,
and then compute the biased distribution we would observe if the children themselves were
asked the question "How many children are in your family?" <br>
Compute the means to observe the difference.

## The Solution
First, I read in the respondent data to variable `resp`.
Then, the column with column label `numkdhh` was isolated by simple indexing. <br>
Using the .Pmf() method, the actual respondent data was constructed into a Pmf object (`actual_pmf`),
which stores unique values and the corresponding probabilities at which they occur. <p>
Moving on to constructing the biased distribution, the pmf object `actual_pmf`
was copied into a separate variable `biased_pmf`. In order to incorporate the inherent bias
existent in surveying children themselves for the number of children in a household, a for loop
was run in which the true probability of a household having *n* children was multiplied by 
the number of children in that household, or *n*. The biased pmf is now normalized so that 
the total probability equals 1. <p>
The two resulting pmfs, `actual_pmf` and `biased_pmf` can now be plotted using `thinkplot` methods,
and their respective means can be computed using the method `.Mean()`.

## The Code

    import nsfg
    import thinkstats2
    import thinkplot
    
    # constructing actual distribution
    resp = nsfg.ReadFemResp()
    num_child = resp['numkdhh']
    actual_pmf = thinkstats2.Pmf(num_child, label = 'Actual')
    
    # constructing biased distribution
    biased_pmf = actual_pmf.Copy(label='Biased')
    for val, prob in biased_pmf.Items():
        biased_pmf.Mult(val, val)
    biased_pmf.Normalize()
    
    # plotting
    thinkplot.PrePlot(2)
    thinkplot.Pmfs([actual_pmf,biased_pmf])
    thinkplot.Show(xlabel = '# of Children',  ylabel='probability')
    
    # computing means
    print('Actual mean', actual_pmf.Mean())
    print('Biased mean', biased_pmf.Mean())
    

