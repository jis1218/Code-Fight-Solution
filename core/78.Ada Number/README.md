Consider two following representations of a non-negative integer:
A simple decimal integer, constructed of a non-empty sequence of digits from 0 to 9;
An integer with at least one digit in a base from 2 to 16 (inclusive), enclosed between # characters, and preceded by the base, which can only be a number between 2 and 16 in the first representation. For digits from 10 to 15 characters a, b, ..., f and A, B, ..., F are used.
Additionally, both representations may contain underscore (_) characters; they are used only as separators for improving legibility of numbers and can be ignored while processing a number.
Your task is to determine whether the given string is a valid integer representation.
Note: this is how integer numbers are represented in the programming language Ada.
Example
For line = "123_456_789", the output should be
adaNumber(line) = true;
For line = "16#123abc#", the output should be
adaNumber(line) = true;
For line = "10#123abc#", the output should be
adaNumber(line) = false;
For line = "10#10#123ABC#", the output should be
adaNumber(line) = false;
For line = "10#0#", the output should be
adaNumber(line) = true;
For line = "10##", the output should be
adaNumber(line) = false.


```java
boolean adaNumber(String line) {
    int a;
        
    if(!line.contains("#")){
        return line.matches("([0-9]_*)+");
    }else{
        try{
            String temp = line.substring(0, line.indexOf("#"));
            temp = temp.replace("_","");
            a = Integer.parseInt(temp);
            System.out.println(a);
        }catch(Exception e){
            return false;
        }
        char small;
        String sma = "";
        char big;
        String bi = "";
        if(a>=11){
            small = (char) (a + 86);
            sma = "a-" + small;
            big = (char) (a + 54);
            bi = "A-" + big;
            a=10;
        }        
        
        //if(line.substring(0,line.lastIndexOf("#")).)
        //System.out.println("((_*[2-9]_*)|_*1_*[0-6]_*)#([0-" + (a-1) + sma + bi + "]_*)+#");
        //System.out.println("((_*[2-9]_*)|_*1_*[0-6]_*)#([0-" + (a-1) + sma + bi + "]_*)+#");
        
        return line.matches("((_*[2-9]_*)|_*1_*[0-6]_*)#(_*[0-" + (a-1) + sma + bi + "]_*)+#");
    }

}
```

##### 정규식 공부

위에서 line.matches("([0-9]_*)+")을 뜯어보면 0부터 9까지는 무조건 1개 이상이어야 하고 _는 있어도 되고 없어도 된다. 즉 3__은 되지만 __만 있는 것은 안된다.

(?=X) X 앞으로 기준, (?!X) X 앞으로 기준이나 그 문자를 제외한 나머지, 후방은 (?<=X), ?에 <와 !를 쓰면 된다.
```java
// example
String b = "12#10001";
for(String str : b.split("(.{1}(?=#))")){
			System.out.println(str);
		}
// 결과는 1, #10001
```

##### 고수의 풀이는 과연 어떨까?
```java
boolean adaNumber(String line) {
    line = line.replaceAll("_", "");
        if(line.matches("^\\d+$")) {
            return true;
        }
        if(line.matches("^\\d+#[0-9a-fA-F]+#")) {
            String[] parts = line.split("#");
            try {
                int base = Integer.parseInt(parts[0]);
                if(base < 2 || base > 16) {
                    return false;
                }
                new BigInteger(parts[1], base);
                return true;
            }
            catch(NumberFormatException e) {
                return false;
            }
        }
        return false;
}
```
##### "_"을 먼저 replace 하는 방법을 많이 사용하였다. 그리고 대부분 정규식을 많이 사용하였다.






