##### 많이 배울 수 있었던 문제였다.

##### 1. java OutOfMemoryError가 일어나는 사례를 볼 수 있었다.
##### 2. prefix algorithm에 대해 아는 계기가 되었다. (이중 포문을 쓸 경우 시간이 엄청 걸림)

```java
int sumInRange(int[] nums, int[][] queries) {
    
    int[] prefixSum = new int[nums.length];
    int[] start = new int[nums.length];
    int[] end = new int[nums.length];
    prefixSum[0] = nums[0];
    for(int i=1; i<nums.length; i++){
        prefixSum[i] = (prefixSum[i-1]+nums[i])%1000000007;
    }
    int sum=0;
    int minus=0;
    for(int i=0; i<queries.length; i++){
        sum = sum%1000000007 + prefixSum[queries[i][1]];
        if(queries[i][0]!=0){
            minus= minus%1000000007+prefixSum[queries[i][0]-1];
        }        
    }
    sum = (sum-minus)%1000000007;
    
    return sum>=0?(int)sum:(int)(1000000007+sum);
}
```


##### 아래와 같이 풀면 Caused by: java.lang.OutOfMemoryError: Java heap space 이 뜬다. long store[][] = new long[nums.length][nums.length]; 에서 문제가 되는 것 같다.

```java
int sumInRange(int[] nums, int[][] queries) {
    long sum=0;
    
    long store[][] = new long[nums.length][nums.length];
    for(int i=0; i<queries.length; i++){
        store[queries[i][0]][queries[i][1]]++;
    }
    
    for(int i=0; i<queries.length; i++){
        long temp=0;
        if(store[queries[i][0]][queries[i][1]]>0){
            for(int j=queries[i][0]; j<=queries[i][1]; j++){
                temp+=(long)nums[j];
            }
            sum+=(long)temp*store[queries[i][0]][queries[i][1]];
            store[queries[i][0]][queries[i][1]]=0;
        }
    }       
    return sum>=0?(int)sum:(int)(1000000007+sum);
}
```