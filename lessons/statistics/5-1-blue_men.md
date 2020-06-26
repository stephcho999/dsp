[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

## The Problem
Given that the distribution of heights of US men is approximately normal, 
with μ = 178cm and σ = 7.7cm, what percentage of the US male population has
height between 5'10" and 6'1"?

## The Solution
First, for conformity of units, feet and inches must be converted to centimeters.
At this point, it can be observed that because the distribution of heights is roughly normal,
the `scipy.stats` method `.norm.cdf()` can be used to approximate the distribution
using the given mean and standard deviation. <p>
The percentage of men between the height of 5'10" and 6'1" can alternately be expressed as
the percentage of men under the height of 6'1" subtracted by the percentage of men under
the height of 5'10". If we plug in the corresponding cm values of 6'1" and 5'10"
in the `.norm.cdf()` method, we can obtain the percentage of men under each respective height.
The difference will be the percentage of men in between those heights.

## The Code
    import scipy.stats
    
    # data given in question
    mean = 178
    std = 7.7
    
    # converting requirements to centimeters
    six_one_inches = 6*12 + 1
    five_ten_inches = 5*12 + 10
    inch_to_cm = 2.54
    six_one_cm = six_one_inches * inch_to_cm
    five_ten_cm = five_ten_inches * inch_to_cm
    
    # Converting cm values to CDF values
    below_six_one = scipy.stats.norm.cdf(six_one_cm, loc = mean, scale = std)
    below_five_ten = scipy.stats.norm.cdf(five_ten_cm, loc=mean, scale=std)
    
    # percentage of men between 5'10" and 6'1" is the difference between the respective CDF values
    fraction_men_in_range = below_six_one - below_five_ten
    percent_men_in_range = fraction_men_in_range * 100
    
    print("{:.4f} percent of US men are between five foot ten and six foot one, and can join the Blue Man Group".format(percent_men_in_range))
    

