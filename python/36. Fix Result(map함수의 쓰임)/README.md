Your teacher asked you to implement a function that calculates the Answer to the Ultimate Question of Life, the Universe, and Everything and returns it as an array of integers. After several hours of hardcore coding you managed to write such a function, and it produced a quite reasonable result. However, when you decided to compare your answer with results of your classmates, you discovered that the elements of your result are roughly 10 times greater than the ones your peers got.
You don't have time to investigate the problem, so you need to implement a function that will fix the given array for you. Given result, return an array of the same length, where the ith element is equal to the ith element of result with the last digit dropped.
Example
For result = [42, 239, 365, 50], the output should be
fixResult(result) = [4, 23, 36, 5].

##### map 함수의 쓰임 - map(f, iterable)의 형태로 쓰인다. 입력받은 자료형의 각 요소를 함수 f로 수행한 후 묶어서 리턴해준다.
```python
def fixResult(result):
    def fix(x):
        return x / 10

    return map(fix, result)
```

##### 위의 식을 람다식으로 표현하면 다음과 같다.
```python
return map(lambda x : x/10, result)
```