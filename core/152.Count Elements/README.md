You've been invited to a job interview at a famous company that tests programming challenges. To evaluate your coding skills, they have asked you to parse a given problem's input given as an inputString string, and count the number of primitive type elements within it.

The inputString can be either a primitive type variable or an array (possibly multidimensional) that contains elements of the primitive types.
A primitive type variable can be:

an integer number;
a string, which is surrounded by " characters (note that it may contain any character except ");
a boolean, which is either true or false.
Return the total number of primitive type elements inside inputString.

Example

For inputString = "[[0, 20], [33, 99]]", the output should be
countElements(inputString) = 4;
For inputString = "[ "one", 2, "three" ]", the output should be
countElements(inputString) = 3;
For inputString = "true", the output should be
countElements(inputString) = 1;
For inputString = "[[1, 2, [3]], 4]", the output should be
countElements(inputString) = 4.

```java
int countElements(String inputString) {
    Pattern p = Pattern.compile("\\b\\d+\\b|\\btrue\\b|\".*?\"|\\bfalse\\b");
    Matcher m = p.matcher(inputString);
    int i=0;
    while(m.find()){
        i++;
    }
    return i;

}
```

##### 정규식에서 boundary 설정하면 딱 그 단어 있는 것만 찾아준다.
##### pattern -> "//btrue//b
##### String -> true 는 Match
##### String -> 33true33 은 not match

##### look negative ahead, look negative behind를 쓰면 비슷하게 구현할 수 있다.
##### //btrue//b와 (?<!\\d+)true(?!\\d+)는 같다.