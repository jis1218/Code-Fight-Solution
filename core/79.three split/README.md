You have a long strip of paper with integers written on it in a single line from left to right. You wish to cut the paper into exactly three pieces such that each piece contains at least one integer and the sum of the integers in each piece is the same. You cannot cut through a number, i.e. each initial number will unambiguously belong to one of the pieces after cutting. How many ways can you do it?
It is guaranteed that the sum of all elements in the array is divisible by 3.
Example
For a = [0, -1, 0, -1, 0, -1], the output should be
threeSplit(a) = 4.
Here are all possible ways:
[0, -1] [0, -1] [0, -1]
[0, -1] [0, -1, 0] [-1]
[0, -1, 0] [-1, 0] [-1]
[0, -1, 0] [-1] [0, -1]
```java
int threeSplit(int[] a) {
    int sum1 = 0;
    int sum2 = 0;
    int sum3 = 0;
    int count = 0;
    
    for(int i=0; i<a.length-2; i++){
        
        sum1 += a[i];        
        sum2 = 0;
        
        for(int j=i+1; j<a.length-1; j++){            
            sum2 += a[j];            
            sum3 = 0;
            if(sum1==sum2){ //sum1과 sum2가 같을 때에만 3번째 계산을 함, 이 if문을 쓰지 않으면 time exceed error 발생
                for(int k=j+1; k<a.length; k++){                
                sum3 += a[k];                  
                }
                
                if(sum1==sum2 && sum2==sum3) count++;
            }                   
        }
    }
    
    return count;
}
```

##### 아래 풀이도 상당히 참신한 풀이... 3개가 같으려면 전부 다 더해 3으로 나눴을 때 하나의 값과 같아야 함
```java
int threeSplit(int[] a) {
    int sum = 0;
    for (int i : a)
        sum += i;
    sum /= 3;
    
    int t = 0;
    int iSum = 0;
    for (int i = 0; i < a.length-2; i++) {
        iSum += a[i];
        if (iSum == sum) {
            int jSum = 0;
            for (int j = i+1; j < a.length-1; j++) {
                jSum += a[j];
                if (jSum == sum)
                    t++;
            }
        }
    }
    return t;
}
```