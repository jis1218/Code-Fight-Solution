CODEWRITING
SCORE: 300/300

Let's say that number a feels comfortable with number b if a ≠ b and b lies in the segment [a - s(a), a + s(a)], where s(x) is the sum of x's digits.
How many pairs (a, b) are there, such that a < b, both a and b lie on the segment [l, r], and each number feels comfortable with the other?
Example
For l = 10 and r = 12, the output should be
comfortableNumbers(l, r) = 2.
Here are all values of s(x) to consider:
s(10) = 1, so 10 is comfortable with 9 and 11;
s(11) = 2, so 11 is comfortable with 9, 10, 12 and 13;
s(12) = 3, so 12 is comfortable with 9, 10, 11, 13, 14 and 15.
Thus, there are 2 pairs of numbers comfortable with each other within the segment [10; 12]: (10, 11) and (11, 12).
```java
int comfortableNumbers(int l, int r) {

    int result = 0;    

    for(int i=l; i<r; i++){
        int ori = i;
        int sum = 0;
        while(ori>0){
            sum += (ori%10);
            ori /= 10;
        }               
        for(int j=1; j<=Math.min(sum,r-i); j++){            
            int gin = i+j;
            int hap = 0;
            while(gin>0){
                hap += gin%10;
                gin /= 10;
            }            
            if(j-hap<=0){
                result++;
            }            
        }            
    }    
    return result;
}
```

##### 다른 풀이 - 공통되는 부분을 함수로 뺐다. 나의 풀이와 크게 다른점이 없는 듯 하다.
```java
int comfortableNumbers(int L, int R) {
    int t = 0;
    for (int a = L; a <= R; a++) {
        for (int b = a+1; b <= R; b++) {
            if (b <= a + digitSum(a) && a >= b - digitSum(b))
                t++;
        }
    }
    return t;
}

int digitSum (int a) {
    if (a < 1)
        return 0;
    return (a%10 + digitSum(a/10));
}
```
