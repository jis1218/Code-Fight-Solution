It frustrates you more than you'd like to admit that the modulus operator in Python can be applied to non-integer values. When you write code, you expect the result of the modulus operator to always be an integer, but thanks to Python this isn't always the case.
To fix this, you've decided to write your own modulus operator as a function. Your task is to implement a function that, given a number n, returns -1 if this number is not an integer and n % 2 otherwise. It is guaranteed that if the number represents an integer, it will be written without a decimal point.

##### python에서는 변수가 항상 int 형이 아니므로 modulus를 구할 때 어려움이 있어 사용자가 직접 구현을 해줘야 한다.
```python
def modulus(n):
    if n == int(n) :
        return n % 2
    else:
        return -1
```

##### 다른 풀이
```python
def modulus(n):
    if type(n) is int:
        return n % 2
    else:
        return -1
```