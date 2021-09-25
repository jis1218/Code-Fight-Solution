Given an integer array nums of length n and an integer target, find three integers in nums such that the sum is closest to target.

Return the sum of the three integers.

You may assume that each input would have exactly one solution.

 

Example 1:

Input: nums = [-1,2,1,-4], target = 1
Output: 2
Explanation: The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
Example 2:

Input: nums = [0,0,0], target = 1
Output: 0

##### 단순히 3중 for문으로 풀었음...

```java
class Solution {
    public int threeSumClosest(int[] nums, int target) {        
       
        int num = nums[0] + nums[1] + nums[2];
        int min = Math.abs(num-target);
        
        for(int i=0; i<nums.length; i++) {
            for(int j=i+1; j<nums.length; j++) {
                int two = i+j;
                for(int k=j+1; k<nums.length; k++) {
                    int temp = nums[i]+nums[j]+nums[k];
                    if(Math.abs(temp-target) < min) {
                        min = Math.abs(temp-target);
                        num = temp;                        
                    }
                }
            }
        }
        
        return num;
    }
}
```

##### 가장 많은 추천을 받은 풀이, 하나만 고정해놓고 나머지 두개는 위 아래로 움직이네...
```java
public int threeSumClosest(int[] num, int target) {
        int result = num[0] + num[1] + num[num.length - 1];
        Arrays.sort(num);
        for (int i = 0; i < num.length - 2; i++) {
            int start = i + 1, end = num.length - 1;
            while (start < end) {
                int sum = num[i] + num[start] + num[end];
                if (sum > target) {
                    end--;
                } else {
                    start++;
                }
                if (Math.abs(sum - target) < Math.abs(result - target)) {
                    result = sum;
                }
            }
        }
        return result;
    }
```