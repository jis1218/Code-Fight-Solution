##### reduce의 쓰임(텐서플로우의 reduce_sum이나 reduce_mean을 떠올려보자)
##### reduce(function, iterable) 형태이다. iterable에 있는 값을 function 처리하여 하나의 값으로 나타내준다.
You need to sum up a bunch of fractions that have different denominators. In order to do this, you need to find the least common denominator of all the fractions. As a professional programmer, you know that the least common denominator is in fact their LCM.
For the given list of denominators, find the least common denominator by finding their LCM.
Example
For denominators = [2, 3, 4, 5, 6], the output should be
leastCommonDenominator(denominators) = 60.

```python
from fractions import gcd

def leastCommonDenominator(denominators):
    return reduce(lambda x, y : x*y/gcd(x,y), denominators)
```
