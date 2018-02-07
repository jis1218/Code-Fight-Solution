Given a positive integer number and a certain length, we need to modify the given number to have a specified length. We are allowed to do that either by cutting out leading digits (if the number needs to be shortened) or by adding 0s in front of the original number.
Example
For number = 1234 and width = 2, the output should be
integerToStringOfFixedWidth(number, width) = "34";
For number = 1234 and width = 4, the output should be
integerToStringOfFixedWidth(number, width) = "1234";
For number = 1234 and width = 5, the output should be
integerToStringOfFixedWidth(number, width) = "01234".
```java
String integerToStringOfFixedWidth(int number, int width) {
    if(width<String.valueOf(number).length()){
        return String.valueOf(number).substring(String.valueOf(number).length()-width);
    }else{
        String res = String.valueOf(number);
        for(int i=0; i<width-String.valueOf(number).length(); i++){
            res = "0" + res;
        }
        return res;        
    }
}
```