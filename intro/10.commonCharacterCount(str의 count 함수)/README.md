Given two strings, find the number of common characters between them.
Example
For s1 = "aabcc" and s2 = "adcaa", the output should be
commonCharacterCount(s1, s2) = 3.
Strings have 3 common characters - 2 "a"s and 1 "c".

##### str의 count 함수를 이용하자
```python
def commonCharacterCount(s1, s2):
    return sum([min((s1.count(s), s2.count(s))) for s in list(set(s1+s2))])
```
