You have been given a string s, which is supposed to be a sentence. However, someone forgot to put spaces between the different words, and for some reason they capitalized the first letter of every word. Return the sentence after making the following amendments:
Put a single space between the words.
Convert the uppercase letters to lowercase.
Example
For s = "CodefightsIsAwesome", the output should be
amendTheSentence(s) = "codefights is awesome";
For s = "Hello", the output should be
amendTheSentence(s) = "hello".

```java
String amendTheSentence(String s) {
    
    String[] str = s.split("(?=[A-Z])");
    String result = "";
    for(int i=0; i<str.length; i++){
        result = result.concat(str[i] + " ");
    }
    
    return result.toLowerCase().trim();

}
```
##### String도 join 함수가 있다는 것을 알아두자!
```java
String amendTheSentence(String s) {
    String[] split = s.split("(?=[A-Z])");
    return String.join(" ", split).toLowerCase();
}
```

##### 파이썬 풀이... re.sub라는 함수를 쓴다.
```python
def amendTheSentence(s):
    
    return re.sub("(?=[A-Z])", " ", s).lower().strip()
```