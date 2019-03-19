[Think Stats Chapter 9 Exercise 2](http://greenteapress.com/thinkstats2/html/thinkstats2010.html#toc90) (resampling)

**Exercise:** In Section 9.3, we simulated the null hypothesis by permutation; that is, we treated the observed values as if they represented the entire population, and randomly assigned the members of the population to the two groups.

An alternative is to use the sample to estimate the distribution for the population, then draw a random sample from that distribution. This process is called resampling. There are several ways to implement resampling, but one of the simplest is to draw a sample with replacement from the observed values, as in Section 9.10.

Write a class named `DiffMeansResample` that inherits from `DiffMeansPermute` and overrides `RunModel` to implement resampling, rather than permutation.

Use this model to test the differences in pregnancy length and birth weight. How much does the model affect the results?

*Writing the `DiffMeansResample` class:*

```
class DiffMeansResample(DiffMeansPermute):
    
    def RunModel(self):
        group1 = np.random.choice(self.pool, self.n, replace=True)
        group2 = np.random.choice(self.pool, self.m, replace=True)
        
        return group1, group2
```

*Running the resample tests:*

```
def RunResampleTests(firsts, others):
    
    data = firsts.prglngth.values, others.prglngth.values
    ht = DiffMeansResample(data)
    p_value = ht.PValue(iters=1000)
    print ('Diff Means Resample Pregnancy Length')
    print('P value: ', p_value)
    print('Actual: ', ht.actual)
    print('TS Max: ', ht.MaxTestStat())
    
    data = firsts.totalwgt_lb.dropna().values, others.totalwgt_lb.dropna().values
    ht = DiffMeansResample(data)
    p_value = ht.PValue(iters=1000)
    print('Diff Means Resample Birth Weight')
    print('P value: ', p_value)
    print('Actual: ', ht.actual)
    print('TS Max: ', ht.MaxTestStat())  

RunResampleTests(firsts,others)

Diff Means Resample Pregnancy Length
P value:  0.176
Actual:  0.07803726677754952
TS Max:  0.17545468402251174
Diff Means Resample Birth Weight
P value:  0.0
Actual:  0.12476118453549034
TS Max:  0.11117805782951251
```

*Using resampling instead of permutation appears to have little effect on the results.*
