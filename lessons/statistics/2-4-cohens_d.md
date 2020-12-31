[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

>> pwd

cd ../ThinkStats2-master/code

import pandas as pd

# various options in pandas
pd.set_option('display.max_columns', 30)  
pd.set_option('display.max_rows', 25)  
pd.set_option('display.precision', 3)  

%run 'nsfg.py'  

import nsfg  

df_FemResp = ReadFemResp()  
df_FemPreg = ReadFemPreg()  
CleanFemPreg(df_FemPreg)  

totalwgt_lb = df_FemPreg['totalwgt_lb']  
totalwgt_lb  

birthord = df_FemPreg['birthord']  
birthord  

df_FemPreg.outcome.value_counts().sort_index()  

df_FemPreg.birthwgt_lb.value_counts(sort=False).head(5)  

preg_map = nsfg.MakePregMap(df_FemPreg)  
preg_map  

# live babies
live = df_FemPreg[df_FemPreg.outcome == 1]  

totalwgt_lb_live = live.totalwgt_lb  

first_wgt = totalwgt_lb_live[live.birthord == 1]  

others_wgt = totalwgt_lb_live[live.birthord != 1]  

first_prglenth = live.prglngth[birthord == 1]  
others_prglenth = live.prglngth[birthord != 1]  
print(first_prglenth, others_prglenth)  

# calculate cohen's d
def cohens_d(group1, group2):  
    """  
    function to calculate cohen's d  
    """  
    import math as math  
    mean1 = group1.mean()  
    mean2 = group2.mean()  
    n1 = len(group1)  
    n2 = len(group2) 
    s_pooled = ((n1-1)*mean1 + (n2-1)*mean2) / (n1+n2-2)  
    return (mean1+mean2) / math.sqrt(s_pooled)  

print(cohens_d(first_wgt, others_wgt))  
print(cohens_d(first_prglenth, others_prglenth))  

