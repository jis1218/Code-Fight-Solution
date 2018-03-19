Hint: for loops also have an else clause which executes when the loop completes normally, i.e. without encountering any breaks
Example
For s = [0, 4, 2, 3, 1, 7] and upperBound = 10,
the output should be
mexFunction(s, upperBound) = 5.
5 is the smallest non-negative integer that is not present in s, and it is smaller than upperBound.
For s = [0, 4, 2, 3, 1, 7] and upperBound = 3,
the output should be
mexFunction(s, upperBound) = 3.
The minimum excludant for the given set is 5, but it's greater than upperBound, so the output should be 3.

```python
def mexFunction(s, upperBound):
    found = -1
    for i in range(upperBound):
        if not i in s:
            found = i
            break
    else:
        found = upperBound

    return found
```