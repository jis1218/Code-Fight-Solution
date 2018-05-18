Given the string, check if it is a palindrome.

```python
def checkPalindrome(inputString):
    for i in range(int(len(inputString)/2)):
        if inputString[i] != inputString[-1*i-1]:
            return False
        pass    
    return True;
```

```python
def checkPalindrome(inputString):
    for i in range(int(len(inputString)/2)):
        if inputString[i] != inputString[len(inputString)-i-1]:
            return False
        pass    
    return True;
```

##### 모범풀이
```python
def checkPalindrome(inputString):
    return inputString == inputString[::-1]
```

##### 예전에 처음 프로그래밍 시작했을 때의 풀이... 허접하구나
```java
boolean checkPalindrome(String str) {
    
    int len = str.length();
    String a[] = str.split("");
    String rev[] = new String[len];
    int correct = 0;
    for(int i=0; i<len; i++){
        rev[len-1-i] = a[i];
    }
    
    for(int j=0; j<len; j++){
        if(a[j].equals(rev[j])){
            correct++;
        }
    }
    
    if(correct==len){
        return true;
    }
    
    return false;

}
```

