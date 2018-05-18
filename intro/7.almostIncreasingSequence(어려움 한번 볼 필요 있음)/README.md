Given a sequence of integers as an array, determine whether it is possible to obtain a strictly increasing sequence by removing no more than one element from the array.
Example
For sequence = [1, 3, 2, 1], the output should be
almostIncreasingSequence(sequence) = false;
There is no one element in this array that can be removed in order to get a strictly increasing sequence.
For sequence = [1, 3, 2], the output should be
almostIncreasingSequence(sequence) = true.
You can remove 3 from the array to get the strictly increasing sequence [1, 2]. Alternately, you can remove 2 to get the strictly increasing sequence [1, 3].

##### 최종 답
```python
def almostIncreasingSequence(sequence):
    cnt = 0
    for i in range(len(sequence)-1):
        if sequence[i]>=sequence[i+1]:
            cnt = cnt+1
            if i>0 and i<len(sequence)-2 and sequence[i]>=sequence[i+2] and sequence[i-1]>=sequence[i+1]: cnt=cnt+1
    
    if(cnt>1): return False
    return True
```

##### 최종답 자바 버전 - 결국 파이썬과 자바의 풀이가 다를게 없다. 다른 사람의 풀이는 자바는 접근 방법이 같고 파이썬은 다르다.
```java
boolean almostIncreasingSequence(int[] sequence) {
    
    int index = 0;
    int count = 0;
    
    
    for(int i=0; i<sequence.length-1; i++){
        if(sequence[i]>=sequence[i+1]){
            index = i;
            count++;
        }
    }
    
    if(index>=1 && index+2<sequence.length && sequence[index-1]>=sequence[index+1] && sequence[index]>=sequence[index+2]){
        return false;
    }
    
    if(count>1){
        return false;
    }
    
    return true;
    
    
}
```

##### 다른 사람의 풀이
```python
def almostIncreasingSequence(s):
    return 3> sum((i >= j) + (i >= k) for i, j, k in zip(s, s[1:], s[2:] + [10**6]))
```

##### 이렇게 하니 시간 초과가 생긴다. 아무래도 zip하는 과정에서 시간이 많이 걸리는 듯 하다.
```python
def almostIncreasingSequence(sequence):
    for i in range(len(sequence)):
        co = sequence.copy()
        del(co[i])
        flag = True
        for i,j in zip(co[:-1],co[1:]):
            if i>=j:
                flag = False
                pass
        if flag: return True
    
    return False
```
##### zip함수에서 시간이 많이 걸릴 것 같아 다음과 같이 실행하였는데도 역시나 에러가 난다. 복사하는 과정에서 시간이 걸리는 것 같다.
```python
def almostIncreasingSequence(sequence):
    for i in range(len(sequence)):
        co = sequence.copy()
        del(co[i])
        flag = True
        for i in range(len(co)-1):
            if co[i]>=co[i+1]:
                flag = False
                pass
        if flag: return True
    
    return False
```