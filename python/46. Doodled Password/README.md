Your friend has been doodling during the lecture and wrote down several digits in a circle. You're wondering if these digits might form the password to your friend's computer. You're planning to prank him some time in the future, and hacking into his computer will definitely help. If the digits written in the clockwise order indeed form a password, all you need to do is figure out which digit comes in it first.
Given a list of digits as they are written in the clockwise order, find all other combinations the password could possibly have.
Example
For digits = [1, 2, 3, 4, 5], the output should be
doodledPassword(digits) = [[1, 2, 3, 4, 5], [2, 3, 4, 5, 1], [3, 4, 5, 1, 2],
                           [4, 5, 1, 2, 3], [5, 1, 2, 3, 4]]


##### 나의 풀이...

##### 배운 점

##### 1. enumerate라는 녀석은 딕셔너리 형식으로 반환해준다.(하지만 dictionary가 아닌 enumerate class 이다.)
```python
res = ['a', 'b', 'c']
enumerate(res)>> [(1, 'a'), (2, 'b'), (3, 'c')]
```
##### 따라서 아래 람다식을 쓸 때 그냥 i, x가 아닌 (i, x)로 해주어야 인자를 받을 수가 있다.
```python
from collections import deque

def doodledPassword(digits):
    n = len(digits)
    res = [deque(digits) for _ in range(n)]
    map(lambda (i,x) : x.rotate(-1*i) , enumerate(res))
    return [list(d) for d in res]
```

##### 다른 괜찮은 풀이를 살펴보자
```python
from collections import deque

def doodledPassword(digits):
    n = len(digits)
    res = [deque(digits) for _ in range(n)]
    map(lambda i: res[i].rotate(-i), range(n))
    return [list(d) for d in res]
```