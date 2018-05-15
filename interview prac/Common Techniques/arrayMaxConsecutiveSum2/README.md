Given an array of integers, find the maximum possible sum you can get from one of its contiguous subarrays. The subarray from which this sum comes must contain at least 1 element.
Example
For inputArray = [-2, 2, 5, -11, 6], the output should be
arrayMaxConsecutiveSum2(inputArray) = 7.
The contiguous subarray that gives the maximum possible sum is [2, 5], with a sum of 7.
#####
```java
int arrayMaxConsecutiveSum2(int[] inputArray) {
    int max = inputArray[0];
    for(int i=0; i<inputArray.length; i++){
        int sum=inputArray[i];
        for(int j=i+1; j<inputArray.length; j++){
            if(sum+inputArray[j]<0) break;
            else{
                sum+= inputArray[j];
                if(max<sum) max = sum;
            } 
        }
        if(max<sum) max = sum;                
    }    
    return max;
}
```

##### 첫번째 풀이었는데 다음과 같은 사항을 고려했어야 한다. ex[3, 2, 4, -1, -1]

```java
int arrayMaxConsecutiveSum2(int[] inputArray) {
    int max = inputArray[0];
    for(int i=0; i<inputArray.length; i++){
        int sum=inputArray[i];
        for(int j=i+1; j<inputArray.length; j++){
            if(sum+inputArray[j]<0) break;
            else sum+= inputArray[j];
        }
        if(max<sum) max = sum;        
    }    
    return max;
}
```

##### 다른 사람의 풀이인데 정말 괜찮은 것 같다. for문도 하나다.
```java
int arrayMaxConsecutiveSum2(int[] inputArray) {
    int max = inputArray[0];
    int cur = max;
    for(int i = 1 ; i < inputArray.length ; i++){
        cur = Math.max(inputArray[i],inputArray[i]+cur);
        max = Math.max(cur,max);
    }
    return max;
}
```