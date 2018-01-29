A media access control address (MAC address) is a unique identifier assigned to network interfaces for communications on the physical network segment.
The standard (IEEE 802) format for printing MAC-48 addresses in human-friendly form is six groups of two hexadecimal digits (0 to 9 or A to F), separated by hyphens (e.g. 01-23-45-67-89-AB).
Your task is to check by given string inputString whether it corresponds to MAC-48 address or not.
Example
For inputString = "00-1B-63-84-45-E6", the output should be
isMAC48Address(inputString) = true;
For inputString = "Z1-1B-63-84-45-E6", the output should be
isMAC48Address(inputString) = false;
For inputString = "not a MAC-48 address", the output should be
isMAC48Address(inputString) = false.

```java
boolean isMAC48Address(String inputString) {
    int j=0;
    if(inputString.length()!=17){
        return false;
    }
    for(int i=0; i<inputString.length(); i++){
        char a = inputString.charAt(i);
        if(i==3*j+2){
            if(a!='-'){
                return false;
            }
            j++;
        }else if(!(('0'<=a && '9'>=a) || ('A'<=a && 'F'>=a))){
            return false;
        }
    }    
    return true;
}
```

##### 정규식을 이용한 풀이
```java
boolean isMAC48Address(String inputString) {
return inputString.matches("([0-9A-F]{2}-){5}[0-9A-F]{2}");
}
```