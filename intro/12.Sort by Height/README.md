Some people are standing in a row in a park. There are trees between them which cannot be moved. Your task is to rearrange the people by their heights in a non-descending order without moving the trees.
Example
For a = [-1, 150, 190, 170, -1, -1, 160, 180], the output should be
sortByHeight(a) = [-1, 150, 160, 170, -1, -1, 180, 190].
##### 파이썬 다른 사람 풀이... 나였으면 이렇게 안풀고 자바와 똑같이 풀었을 것이다.
```python
def sortByHeight(a):

    l = sorted([i for i in a if i > 0])
    for n,i in enumerate(a):
        if i == -1:
            l.insert(n,i)
    return l
```
```python
def sortByHeight(a):
    people = [n for n in a if n != -1]
    people.sort()
    for i in range(len(a)):
        a[i] = people.pop(0) if a[i] != -1 else a[i]
    return a
```

```java
int[] sortByHeight(int[] a) {
    for(int i=0; i<a.length; i++){
        if(a[i]!=-1){
        for(int j=i+1; j<a.length; j++){
          if(a[j]!=-1)  
            if(a[i]>a[j]){                
                int temp = a[i];
                a[i] = a[j];
                a[j] = temp;                
            }
        } 
        }        
    }    
    return a;
}
```