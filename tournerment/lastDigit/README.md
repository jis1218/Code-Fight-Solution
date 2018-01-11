For given integers a and b, find the last digit of ab.
Example
For a = 2 and b = 5, the output should be
lastDigit(a, b) = 2.
Explanation: 25 = 32.
##### 원래 풀이
```java
int lastDigit(int a, int b) {
    return (int) Math.pow(a,b)%10;
}
```
##### 이 풀이로 하면 b가 엄청 커질 경우 잘못된 값이 나오게 된다.
##### 그래서 잘 된 풀이를 따라 쳐보았다.
```java
int lastDigit(int a, int b) {
    int r = 1;
    for(int i=1; i<=b; i++){
        r = (r*a)%10;
    }

    return r;
}
```

##### 원래 풀이에서 좀 수정하면 아래 코드도 가능하다.
```java
int lastDigit(int a, int b) {

    if(b==0){
        return 1;
    }

    int i = a%10;
    int j = b%4+4; // b를 4로 나눈 이유는 1~9 사이에 어떤 수든 2번 또는 4번 주기로 같은 숫자가 나타난다.

    return (int) Math.pow(i,j)%10;
}
```
