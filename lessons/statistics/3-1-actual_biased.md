[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

pwd  

cd ../ThinkStats2-master/code  

from __future__ import print_function, division  

%matplotlib inline  

import numpy as np  

import nsfg  
import first  
import thinkstats2  
import thinkplot  

preg = nsfg.ReadFemPreg()  
live = preg[preg.outcome == 1]  

d = { 7: 8, 12: 8, 17: 14, 22: 4,  
     27: 6, 32: 12, 37: 8, 42: 3, 47: 2 }  

pmf = thinkstats2.Pmf(d, label='actual')  
pmf  

def BiasPmf(pmf, label):  
    new_pmf = pmf.Copy(label=label)  

    for x, p in pmf.Items():  
        new_pmf.Mult(x, x)  
        
    new_pmf.Normalize()  
    return new_pmf  

biased_pmf = BiasPmf(pmf, label='observed')  
[biased_pmf, pmf]  
biased_pmf.Mean()  

thinkplot.PrePlot(2)  
thinkplot.Pmfs([pmf, biased_pmf])  
thinkplot.Show(xlabel='class size', ylabel='PMF')  

df_FemResp = nsfg.ReadFemResp()  


numkdhh = df_FemResp.numkdhh  
numkdhh.describe()  

pmf = thinkstats2.Pmf(numkdhh, label='actual')  
pmf  

biased_pmf = BiasPmf(pmf, label='observed')  
biased_pmf  

thinkplot.PrePlot(2)  
thinkplot.Pmfs([pmf, biased_pmf])  
thinkplot.Show(xlabel='class size', ylabel='PMF')  

# calculate mean values:
# the sum of the numbers of children x their respective pmf value
print(pmf.Mean(), biased_pmf.Mean())  

