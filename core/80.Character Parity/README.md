Given a character, check if it represents an odd digit, an even digit or not a digit at all.
Example
For symbol = '5', the output should be
characterParity(symbol) = "odd";
For symbol = '8', the output should be
characterParity(symbol) = "even";
For symbol = 'q', the output should be
characterParity(symbol) = "not a digit".

##### 메모리 측면에서 좋은 풀이는 아니다.
```java
String characterParity(char symbol) {
    int a = 0;
    try{
        a = Integer.parseInt(symbol+"");
    }catch(Exception e){
        return "not a digit";
    }
    
    if(a%2==0) return "even";
    else return "odd";
       
}
```
##### 이상적인 풀이
```java
String characterParity(char symbol) {
    if (symbol < '0' || symbol > '9')
        return "not a digit";
    if ((symbol - '0')%2 == 0) //char-char해서 int를 얻어낸다.
        return "even";
    return "odd";
}
```
