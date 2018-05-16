
##### 나의 풀이
```java
int[] findLongestSubarrayBySum(int s, int[] arr) {
    int[] prefixSum = new int[arr.length+1];
    int[] sumMinus = new int[arr.length+1];
    prefixSum[0] = 0;
    sumMinus[0] = arr[0]-s;
    int maxLen = -1;
    int start = 0;
    int end = 0;
    int index = 0;
    
    for(int i=0; i<arr.length; i++){
        prefixSum[i+1] = prefixSum[i] + arr[i];
        sumMinus[i+1] = prefixSum[i+1]-s;
    }
    
    for(int i=0; i<prefixSum.length; i++){
        if(sumMinus[i]>=0){
            for(int j=index; j<arr.length; j++){
                if(sumMinus[i]==prefixSum[j]){
                    if(i-j>maxLen){
                        maxLen = i-j;
                        end = i;
                        start = j+1;
                        index = j;
                        break;
                    }                    
                }else if(sumMinus[i]<prefixSum[j]){
                    index=j;
                    break;
                } 
            }            
        }                
    }
    return maxLen==-1?new int[]{-1}:new int[]{start, end};
}
```

##### 다른 사람의 풀이
```java
int[] findLongestSubarrayBySum(int s, int[] arr) {
    int[] longest = new int[]{-1, -2};
    
    int left = 0, right = 0;
    int sum = 0;
    
    while (right < arr.length) {
        sum += arr[right];
        
        while (sum > s && left <= right) sum -= arr[left++];
        
        if (sum == s && right - left > longest[1] - longest[0]) {
            longest[0] = left+1;
            longest[1] = right+1;
        }
        
        right++;
    }
    
    if (longest[0] == -1 || longest[1] == -1) return new int[]{-1};
    
    return longest;
}
```