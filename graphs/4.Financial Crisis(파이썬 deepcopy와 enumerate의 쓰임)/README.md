Once upon a time, in a kingdom far, far away, there lived a king Byteasar IV. As Interkingdomial financial crisis was roaring through the neighborhood, Byteasar was struggling with keeping the economy out of recession. Unfortunately there was not much he could do. After long and deep thinking, the king came to the only solution: one of his cities should be demolished, since keeping communication between all the cities is way too expensive.
It is not yet known if Byteasar chose the city to destroy after a careful planning or picked one at random. As a person with PhD in history and Nobel prize in Computer Science, you can solve this mystery. Archaeologists have recently found a manuscript with the information about the roads between the cities, that is now stored in the roadRegister matrix. You want to try and remove each city one by one and compare the road registers obtained this way. Thus you'll be able to compare the obtained roads and determine whether the one picked by Byteasar was the best by some criteria.
Given the roadRegister, return an array of all the road registers obtained after removing each of the city one by one.
```java
boolean[][][] financialCrisis(boolean[][] r) {
    boolean[][][] result = new boolean[r.length][r.length-1][r.length-1];
    for(int i=0; i<r.length; i++){
        int jj=0;        
        for(int j=0; j<r.length; j++){
            int kk=0;
            if(j!=i){
                for(int k=0; k<r.length; k++){
                    if(k!=i){
                        result[i][jj][kk] = r[j][k];
                        kk++;
                    } 
                }
                jj++;
            } 
        }
    }
    return result;
}
```

##### 다른 풀이에서 괜찮은 부분
```java
results[i][j][k] = roadRegister[j+(j>=i?1:0)][k+(k>=i?1:0)];
```


```python
import copy
def financialCrisis(roadRegister):
    result=[]
    
    for i in range(len(roadRegister)):
        copyR = copy.deepcopy(roadRegister)
        print(roadRegister)
        for j in range(len(roadRegister)):
            print(i, j)
            del(copyR[j][i])
        
        del(copyR[i])
        print(copyR)
        result.append(copyR)
    return result
```

```python
def financialCrisis(roadRegister):
    result = []
    for k in range(len(roadRegister)):
        result.append([[roadRegister[i][j] for j in range(len(roadRegister)) if j!=k] for i in range(len(roadRegister)) if i!=k])
    return result
```

##### 파이썬에서 이렇게도 할 수 있구나
```python
def financialCrisis(A):
    N = len(A)
    return [ [row[:k] + row[k+1:] for r,row in enumerate(A) if r != k]
             for k in xrange(N) ]
```