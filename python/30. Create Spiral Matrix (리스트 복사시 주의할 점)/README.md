##### 풀이
```python
def createSpiralMatrix(n):
    dirs = [(-1, 0), (0, -1), (1, 0), (0, 1)]
    curDir = 0
    curPos = (n - 1, n - 1)
    res = [[0 for x in range(n)] for x in range(n)] #List Comprehension을 이용해야 함
    print(res)

    for i in range(1, n * n + 1):
        res[curPos[0]][curPos[1]] = i
        nextPos = curPos[0] + dirs[curDir][0], curPos[1] + dirs[curDir][1]
        if not (0 <= nextPos[0] < n and
                0 <= nextPos[1] < n and
                res[nextPos[0]][nextPos[1]] == 0):
            curDir = (curDir + 1) % 4
            nextPos = curPos[0] + dirs[curDir][0], curPos[1] + dirs[curDir][1]
        curPos = nextPos

    return res
```

##### 오답풀이 - 왜 위에랑 다른걸까??
```python
res = [[0]*n]*n
```

##### 그 이유는 다음과 같다.
##### Just remember that [0]*n creates n references to one object (that's why all the instances update their values when one is modified). So, you can try using list comprehension for this task

##### 즉 *n 식으로 list를 복사하게 되면 레퍼런스도 같이 바뀌므로 하나의 값이 바뀔때 다른 값까지 모두 바뀌게 된다.
##### 실험

```python
test = [0]*3
test[0] = 1
print(test) # [1, 0, 0]

res = [[0]*3]*3
res[0][0] = 1


print(test) # [[1, 0, 0], [1, 0, 0], [1, 0, 0]]
```