Given an array of strings, return another array containing all of its longest strings.
Example
For inputArray = ["aba", "aa", "ad", "vcd", "aba"], the output should be
allLongestStrings(inputArray) = ["aba", "vcd", "aba"].

```python
def allLongestStrings(inputArray):
    max=len(inputArray[0])
    a = []
    for i in inputArray:
        if len(i)>max:
            a.clear()
            max = len(i)
            a.append(i)
        elif len(i)==max:
            a.append(i)
    
    return a
```

##### 배우자 쫌!!!!
```python
def allLongestStrings(inputArray):
    m = max(len(s) for s in inputArray)
    r = [s for s in inputArray if len(s) == m]
    return r
```