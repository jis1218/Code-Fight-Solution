You are planning to rob houses on a specific street, and you know that every house on the street has a certain amount of money hidden. The only thing stopping you from robbing all of them in one night is that adjacent houses on the street have a connected security system. The system will automatically trigger an alarm if two adjacent houses are broken into on the same night.
Given a list of non-negative integers nums representing the amount of money hidden in each house, determine the maximum amount of money you can rob in one night without triggering an alarm.
Example
For nums = [1, 1, 1], the output should be
houseRobber(nums) = 2.
The optimal way to get the most money in one night is to rob the first and the third houses for a total of 2.

##### 내 풀이에도 박수를 보내고 싶지만...
```java
int houseRobber(int[] nums) {
   if(nums.length==0) return 0;
   if(nums.length==1) return nums[0];
   int [] maximum = new int[nums.length]; //특정 위치에서의 maximum 값을 받는 배열

   return Math.max(helper(nums, 0, 0, maximum), helper(nums, 1, 0, maximum));
}

int helper(int[] nums, int start, int max, int[] maximum){
   if(nums.length-start<1) return max;
   max += nums[start];
   System.out.println(nums[start] + ", max=" + max);
   
   //만약 특정 위치에서의 최대값보다 max값이 크지 않으면 그 재귀함수는 끝나게 된다.
   if(maximum[start]<max){
      maximum[start]=max;
   }else{
      return 0;
   }
   
   int a = helper(nums, start+2, max, maximum);
   int b = helper(nums, start+3, max, maximum);
   
   return Math.max(a, b);
}
```

##### 그뤠잇
```java
int houseRobber(int[] h) {
    int a = 0, b = 0;
    
    for (int m : h) {
        b = Math.max(m + a, a = b);
    }
    
    return b;
}
```

##### python으로 발버둥 쳤으나 나름 메모아이제이션까지 썼으나...
```python
def getMax(nums, index, memo):
    
    if index<0 :
        return 0
    if index==0 or index==1 :
        return nums[index]
    if memo[index]==None:
        memo[index] = max(nums[index]+getMax(nums, index-2, memo), nums[index]+getMax(nums, index-3, memo))
    return memo[index]

def houseRobber(nums):
    memo = [None]*len(nums)
    if len(nums)==0 : return 0
    if len(nums)==1 : return nums[0]
    return max(getMax(nums, len(nums)-1, memo), getMax(nums, len(nums)-2, memo))
```
##### 위의 풀이를 따라갈 수는 없구나 쉽게 생각하기 어려운 풀이