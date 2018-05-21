Ticket numbers usually consist of an even number of digits. A ticket number is considered lucky if the sum of the first half of the digits is equal to the sum of the second half.
Given a ticket number n, determine if it's lucky or not.
Example
For n = 1230, the output should be
isLucky(n) = true;
For n = 239017, the output should be
isLucky(n) = false.

##### sum함수는 숫자만 계산할 수 있음
```python
def isLucky(n):
    a = str(n)
    b = int(len(a)/2)
    return sum([int(i) for i in a[:b]]) == sum([int(i) for i in a[b:]])
```

##### int도 함수이기 때문에 map을 써서 다음과 같이 나타낼 수도 있음
```python
def isLucky(n):
    s = str(n)
    pivot = len(s)//2
    left, right = s[:pivot], s[pivot:]
    return sum(map(int, left)) == sum(map(int, right))
```

##### 옛날 나의 풀이
```java
boolean isLucky(int n) {
        
        String str = String.valueOf(n);
        int len = str.length();
    if(len%2==1){
        return false;
    }else{     
        
        int[] arr = new int[len];
        int sum=n;
        for(int i=0; i<len; i++){
            arr[i] = sum%10;
                sum = sum/10;
                  
            
        }
        
            int firstSum = 0;
        int secondSum = 0;
        for(int i=0; i<len/2; i++){
            firstSum = firstSum + arr[i];
            secondSum = secondSum + arr[i+len/2];
        }
        
        if(firstSum==secondSum){
            return true;
        }
        
        return false;
    }

}
```
##### string의 charAt을 쓴 것이 기발하다.
```java
boolean isLucky(int n) {

    String s = n+"";
    int sum = 0;
    
    for(int i=0; i<s.length()/2; i++)
        sum+=(s.charAt(i)-s.charAt(s.length()-1-i));
    
    return sum==0;
}
```