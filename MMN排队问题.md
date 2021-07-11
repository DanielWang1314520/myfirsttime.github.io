**MMN排队问题**

```python
`# -*- coding: utf-8 -*-
"""
Created on Sat May 29 16:43:05 2021

@author: win10

排队程序，M/M/N/无穷 问题
输入服务员个数N，得到的队伍长度为L
"""
from math import *

def getLength(n,lmd,mu):
    #计算rho
    rho = lmd/mu
    #先计算p_0
    sum_p = 0
    for i in range(n):
        sum_p = sum_p +rho**i/factorial(i)
    s_n=rho**n/factorial(n)
    sum_n=sum_p+s_n
    sum_s=sum_n+(rho/n)/(1-rho/n)

    p_0=1/sum_s
    #计算队列长度length(在前后项差值小于0.00001时停下)
    length=0
    for i in range(n):
        length=length+i*rho**i/factorial(i)*p_0
    p_length = length
    length=length + n*rho**n/factorial(n)*p_0
    p_n=rho**n/factorial(n)*p_0
    i=1
    while length-p_length>0.001:
        p_length=length
        length=length+(i+n)*(rho/n)**i*p_n
        i+=1
    return length

if __name__=="__main__":
    n = int(input("请输入服务员的个数N："))
    print("----注意：lambda小于N*mu，且二者均在0与1之间----")
    lmd = float(input("请输入顾客在单位时间deta(t)内进队的速度（平均个数）lambda："))
    mu = float(input("请输入每个服务员在单位时间内处理顾客的速度（平均个数）mu："))
    result = getLength(n,lmd,mu)
    res_int = int(result)
    print("\n计算的队长结果为：",result,"\n")
    print("\n四舍五入为：",res_int,"\n")`
```



