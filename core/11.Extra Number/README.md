You're given three integers, a, b and c. It is guaranteed that two of these integers are equal to each other. What is the value of the third integer?
Example
For a = 2, b = 7 and c = 2, the output should be
extraNumber(a, b, c) = 7.
The two equal numbers are a and c. The third number (b) equals 7, which is the answer.

```java
int extraNumber(int a, int b, int c) {
    if(a!=b){
        if(a==c){
            return b;
        }else{
            return a;
        }
    }else{
        return c;
    }
}
```

##### 최고의 풀이
```java
int extraNumber(int a, int b, int c) {
    return a^b^c;
}
```
##### java에서 ^는 XOR을 나타낸다. a와 b와 c를 2진법으로 나타낸 후 ^를 사용하면 같은 수는 0이 된다. ex) a=30, b=30이면 a^b는 0이 된다. 여기에 c^0하면 c가 된다.

##### 또다른 풀이
```java
int extraNumber(int a, int b, int c) {
    return a == b ? c : a == c ? b : a;
}
```
##### 3항 연산자 이용, a==b?c:a를 풀어서 쓰면
```java
if(a==b) return c;
else return a;
```
