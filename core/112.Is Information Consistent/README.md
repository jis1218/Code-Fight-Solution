Example
For
evidences = [[ 0, 1, 0, 1], 
             [-1, 1, 0, 0], 
             [-1, 0, 0, 1]]
the output should be
isInformationConsistent(evidences) = true;
For
evidences = [[ 1, 0], 
             [-1, 0], 
             [ 1, 1],
             [ 1, 1]]
the output should be
isInformationConsistent(evidences) = false.

##### 나의 풀이
```java
boolean isInformationConsistent(int[][] evidences) {
    
    for(int i=0; i<evidences[0].length; i++){
        int pIndex=0;
        int mIndex=0;
        for(int j=0; j<evidences.length; j++){            
            if(evidences[j][i]>0){
                pIndex++;
            }else if(evidences[j][i]<0){
                mIndex++;
            }
            
            if(pIndex>0 && mIndex>0) return false;            
        }
    }
    
    return true;
}
```
##### 괜찮은 풀이
```java
boolean isInformationConsistent(int[][] evidences) {
    for (int i = 0; i < evidences[0].length; i++) {
        int type = 0;
        for (int j = 0; j < evidences.length; j++) {
            if (evidences[j][i] != 0) {
                if (type == 0)
                    type = evidences[j][i];
                if (evidences[j][i] != type)
                    return false;
            }
        }
    }
    return true;
}
```