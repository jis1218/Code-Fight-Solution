For t = 3.1415, width = 10 and precision = 2,
the output should be
competitiveEating(t, width, precision) = "   3.14   ".

```python
def competitiveEating(t, width, precision):
    return ("{0:^" + str(width) + "." + str(precision) + "f}").format(t)
```

##### 다른 풀이
```python
def competitiveEating(t, width, precision):
    return "{0:.{1}f}".format(t,precision).center(width)

def competitiveEating(t, width, precision):
    return ('{:^{w}.{p}f}').format(t,w=width,p=precision)
```