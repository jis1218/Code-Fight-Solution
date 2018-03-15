Now you're bound to win. Implement a function that, given an integer number n and a base x, converts n from base x to base 16.
```python
def baseConversion(n, x):
    return hex(int(n, x))[2:] #파이썬에서는 숫자도 특정 인덱스만 뽑을 수 있다. ex[2:]
```