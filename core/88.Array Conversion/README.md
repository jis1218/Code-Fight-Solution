Given an array of 2k integers (for some integer k), perform the following operations until the array contains only one element:
On the 1st, 3rd, 5th, etc. iterations (1-based) replace each pair of consecutive elements with their sum;
On the 2nd, 4th, 6th, etc. iterations replace each pair of consecutive elements with their product.
After the algorithm has finished, there will be a single element left in the array. Return that element.
Example
For inputArray = [1, 2, 3, 4, 5, 6, 7, 8], the output should be
arrayConversion(inputArray) = 186.
We have [1, 2, 3, 4, 5, 6, 7, 8] -> [3, 7, 11, 15] -> [21, 165] -> [186], so the answer is 186.
##### 나의 풀이
```java
int arrayConversion(int[] inputArray) {
    int index=1;
    
    while(inputArray.length>1){
        int j=0;        
        for(int i=0; i<inputArray.length; i+=2){
            if(index%2==1) inputArray[j] = inputArray[i]+inputArray[i+1];
            else inputArray[j] = inputArray[i]*inputArray[i+1];  
            j++;            
        }
        inputArray = Arrays.copyOfRange(inputArray, 0, inputArray.length/2);
        index++;        
    }    
    return inputArray[0];
}
```
##### 다른 사람 풀이, Arrays.copyRange를 하지 않았다. 주어진 Array를 그대로 살렸다.
```java
int arrayConversion(int[] a) {
    int n = a.length, i = 1;
    
    while (n>1) {
        for (int j = 0; j < n/2; j ++) {
            a[j] = i==1?a[2*j]+ a[2*j+1]:a[2*j]* a[2*j+1];
        }
        n /= 2;
        i = 1-i; // 나름의 toggle을 만드는 방법
    }
    
    return a[0];
}
```