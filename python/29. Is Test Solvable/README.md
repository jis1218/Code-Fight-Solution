You've been preparing all night for the upcoming test and entered the class certain that you will ace it. Now that you received the test questions, you died inside a little: looks like you prepared for the test on a completely different topic.
You're not even sure if you should bother to answer the questions. You still have some hope though: it is known that there's a glitch in the test preparing system, so that if the sum of digits of question ids is divisible by k, the answer to each question has a 90% probability to be an A.
Given the list of question ids, determine if the sum of their digits is divisible by k to see if it's worth trying to pass the test.

```python
def isTestSolvable(ids, k):
    digitSum = lambda i : sum([int(digit) for digit in str(i)])

    sm = 0
    for questionId in ids:
        sm += digitSum(questionId)
    return sm % k == 0
```

##### map도 공부해볼 필요가 있다.
```python
def isTestSolvable(ids, k):
    digitSum = lambda q: sum(map(int, str(q)))

    sm = 0
    for questionId in ids:
        sm += digitSum(questionId)
    return sm % k == 0
```