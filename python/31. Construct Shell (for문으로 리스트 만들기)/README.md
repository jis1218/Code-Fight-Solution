A 2D list lst of size 2 * n - 1 is called a shell if it is filled with zeros and has the following configuration:
lst[0] contains one element;
lst[1] contains two elements;
...
lst[n - 2] contains n - 1 elements;
lst[n - 1] contains n elements;
lst[n] contains n - 1 elements;
...
lst[2 * n - 3] contains two elements;
lst[2 * n - 2] contains one element.
Given an integer n, return a shell list.
Example
For n = 3, the output should be
constructShell(n) = [[0],
                     [0, 0],
                     [0, 0, 0],
                     [0, 0],
                     [0]]

```python
def constructShell(n):
    return [[0 for i in range(k)] for k in ([j for j in range(1, n+1)] + [m for m in range(n-1, 0, -1)])]
```

##### 다른 풀이
```python
def constructShell(n):
    return [[0]*min(i,2*n-i) for i in range(1,2*n)]
```
