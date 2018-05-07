Check if the given string is a correct time representation of the 24-hour clock.
Example
For time = "13:58", the output should be
validTime(time) = true;
For time = "25:51", the output should be
validTime(time) = false;
For time = "02:76", the output should be
validTime(time) = false.

```java
boolean validTime(String time) {
    String[] result = time.split(":");
    int hour = Integer.parseInt(result[0]);
    int min = Integer.parseInt(result[1]);
    if(0<=hour && hour<=23 && 0<=min && 59>=min){
        return true;
    }    
    return false;
}
```
