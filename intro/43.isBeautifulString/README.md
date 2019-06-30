A string is said to be beautiful if each letter of the alphabet appears at most as many times as than the previous letter; ie: b occurs no more times than a; c occurs no more times than b; etc.

Given a string, check whether it is beautiful.

Example

For inputString = "bbbaacdafe", the output should be
isBeautifulString(inputString) = true;

```python
def isBeautifulString(inputString):
    a = [0]*(ord('z')-ord('a')+1)
    
    for word in inputString:
        a[ord(word)-ord('a')]+=1
    
    for i in range(1, len(a)):
        if a[i]>a[i-1]:
            return False
    return True
```

##### 제대로 된 풀이... count 함수를 잘 이용해야 한다.
```python
r = [inputString.count(i) for i in string.ascii_lowercase]
    
    return r[::-1] == sorted(r)
```