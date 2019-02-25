# Java Regex

##### positive lookahead - https://www.logicbig.com/tutorials/core-java-tutorial/java-regular-expressions/regex-lookahead.html
```java
Pattern.compile("\\d+(?=\\scm)")
       .matcher("200 cm")
       .find();//matches:  '200' at 0-3
               //'200 cm'
```

##### positive lookahead의 다른 example
```java
Pattern.compile("(?=[a-z][0-9])[a-z]")
       .matcher("a7 bb")
       .find();//matches:  'a' at 0-1
               //'a7 bb'

/* Our lookahead is: a character followed by a digit followed by a character: but we are only want to have match for first character.*/
Pattern.compile("(?=[a-z][0-9][a-z])[a-z]")
       .matcher("a7a bbb 9z9")
       .find();//matches:  'a' at 0-1
               //'a7a bbb 9z9'

/* This doesn't work, the expression part following the lookahead should start with a character.*/
Pattern.compile("(?=[a-z][0-9])[0-9]")
       .matcher("7a bc d8 9w")
       .find();//no matches

/* This works.*/
Pattern.compile("(?=[a-z][0-9])d[0-9]")
       .matcher("7a bc c6 d8 9w")
       .find();//matches:  'd8' at 9-11
               //'7a bc c6 d8 9w'
```

Rewriting above example: (?=[a-z][0-9])[a-z].
How engines works?
At a given position of the input string, the engine will read the lookahead part '(?=[a-z][0-9])' first. 
For the first part [a-z]: if at the current position of the input string there is a character between a to z then good. 
For Second part [0-9]: if there's a digit at the following position then the current position satisfies the entire lookahead part otherwise it does not. During this time no input sequence is consumed. 
If current input character does not satisfy the lookahead part, the engine will reject the current character as a match and will move on to the next character 
If current input position satisfies the lookahead part then engine will actually apply the match at the current position. The next part of the expression (just after the assertion part) is [a-z]. As we know engine discards all matches of the assertion as soon as it's out of the assertion part (last section discussion) it will match the current input string with the the next '[a-z]' regex part normally. It just like engine doesn't have any memory of the last assertion. The assertion only helped the engine to decided whether the current position should be attempted for a match or not. If no then engine would have moved to next position already.
In our example if at current position we have a character matching '[a-z]' (of course we must have it, that's why assertion passed) then we have a match. 


##### Negative Lookahead
```java
Pattern.compile("[a-z](?![0-9])")
       .matcher("a9 c2 a1 dd")
       .find();//matches:  'd' at 9-10, 'd' at 10-11
               //'a9 c2 a1 **dd**'

// 처음에 a-z를 찾는다.
// 만족하면 0-9가 아닌 문자를 찾는다.
// 그 문자를 만족할 경우 처음에 찾은 a-z를 찾게 된다.
// 첫번째 d는 뒤에 숫자가 아닌 d가 왔기 때문에 Match
// 두번째 d는 뒤에 아무것도 오지 않았기 때문에 Match
```


