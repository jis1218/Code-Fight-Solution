Consider the following ciphering algorithm:
For each character replace it with its code.
Concatenate all of the obtained numbers.
Given a ciphered string, return the initial one if it is known that it consists only of lowercase letters.
Note: here the character's code means its decimal ASCII code, the numerical representation of a character used by most modern programming languages.
Example
For cipher = "10197115121", the output should be
decipher(cipher) = "easy".
Explanation: charCode('e') = 101, charCode('a') = 97, charCode('s') = 115 and charCode('y') = 121.
```java
String decipher(String cipher) {
    String result = "";
    int t = 0;
    for (byte b : cipher.getBytes()) {
        t *= 10;
        t += b - '0';
        if (t >= 'a') {
            if (t > 'z')
                return "";
            result += (char)(t);
            t = 0;
        }
    }
    return result;
}
```