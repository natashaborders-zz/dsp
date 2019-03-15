[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

**Exercise:** In the BRFSS (see Section 5.4), the distribution of heights is roughly normal with parameters µ = 178 cm and σ = 7.7 cm for men, and µ = 163 cm and σ = 7.3 cm for women.

In order to join Blue Man Group, you have to be male between 5’10” and 6’1” (see http://bluemancasting.com). What percentage of the U.S. male population is in this range? Hint: use scipy.stats.norm.cdf.

scipy.stats contains objects that represent analytic distributions

    import scipy.stats

For example scipy.stats.norm represents a normal distribution.

    mu = 178
    sigma = 7.7
    dist = scipy.stats.norm(loc=mu, scale=sigma)
    type(dist)
    scipy.stats._distn_infrastructure.rv_frozen

A "frozen random variable" can compute its mean and standard deviation.

    dist.mean(), dist.std()
    (178.0, 7.7)

It can also evaluate its CDF. How many people are more than one standard deviation below the mean? About 16%

    dist.cdf(mu-sigma)
    0.1586552539314574

How many people are between 5'10" and 6'1"?

*Figuring out the percentage of men below 5'10" in this normal distribution:*

    dist.cdf(177.8)
    0.48963902786483265

*Figuring out the percentage of men below 6'1" in this normal distribution:*

    dist.cdf(185.42)
    0.8323858654963063

*Between these two percentages lie the potential Blue Men:*

    Blue_Men_Potential = (dist.cdf(185.42)-dist.cdf(177.8))
    Blue_Men_Potential
    0.3427468376314737

*This means that 34.27% of men can potentially realize their dreams by joining the Blue Man Group.*
