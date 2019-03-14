[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

#Calculating Cohen's effect size to investigate whether first babies are lighter or heavier than others.

firsts.totalwgt_lb.mean(), others.totalwgt_lb.mean()# the mean weights for both groups

difference = firsts.totalwgt_lb.mean() - others.totalwgt_lb.mean() # the difference in means is negative
# first babies on average appear to be lighter than other babies

variance_firsts = firsts.totalwgt_lb.var()
variance_others = others.totalwgt_lb.var()
n_firsts = len(firsts)
n_others = len(others)

pooled_variance = (n_firsts*variance_firsts + n_others*variance_others)/(n_firsts+n_others)
pooled_stdev = np.sqrt(pooled_variance)
effect_size_d = difference/pooled_stdev

effect_size_d

-0.088672927072602
#the result indicates that the effect size is larger than for the difference in pregnancy length, equal to 0.0887 standard deviations
