Determine if the given number is a power of some non-negative integer.
Example
For n = 125, the output should be
isPower(n) = true;
For n = 72, the output should be
isPower(n) = false.
```java
boolean isPower(int n) {
    int num = 2;

    if(n==1) return true;

    for(int i=2; i<=Math.sqrt(n); i++){
        int origin = n;
        while(true){
            if(origin%i==0){
                origin /= i;
            }else{
                break;
            }
            
            if(origin==i){
                return true;
            }
        }
    }
    return false;
}
```
#### 다른 풀이
```java
boolean isPower(int n) {
    for( int i = 2 ; i < 5 ; i++ ){
        if(Math.round(Math.pow(n , 1f/i) * 1000f) / 1000f % 1 == 0){
            return true;
        };
    }
    return false;
}
```
