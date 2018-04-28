For lst1 = [2, 2, 1] and lst2 = [10, 11], the output should be
listsConcatenation(lst1, lst2) = [2, 2, 1, 10, 11].

```python
def listsConcatenation(lst1, lst2):
    res = lst1
    res.extend(lst2)
    return res
```