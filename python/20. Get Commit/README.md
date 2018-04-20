Example
For commit = "0??+0+!!someCommIdhsSt", the output should be
getCommit(commit) = "someCommIdhsSt".

##### 나의 풀이
```python
def getCommit(commit):
    return str(commit).replace('0', "").replace('?',"").replace('+','').replace('!','')
```

##### 좋은 풀이
```python
def getCommit(commit):
    return commit.lstrip('0?+!')
```