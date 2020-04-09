Write a function that takes a string as input and returns the string with only the vowels reversed.
Note: The letters "a", "e", "i", "o", and "u" are vowels. The letter "y" is not a vowel.

Example

For s = "hello, world", the output should be
reverseVowelsOfString(s) = "hollo, werld";
For s = "codesignal", the output should be
reverseVowelsOfString(s) = "cadisegnol";
For s = "eIaOyU", the output should be
reverseVowelsOfString(s) = "UOaIye".

##### java로 짠 최초의 코드, 스택과 큐를 이용 (기존 코드에서도 그나마 줄인 코드)
```java
String reverseVowelsOfString(String s) {
    String reverseVowelsOfString(String s) {
    int i,j,k,l=s.length();
    var t = "aeiouAEIOU";
    k = l-1;
    var r="";
    for(i=0; i<l; i++){
        var c = s.charAt(i);
        if(t.contains(""+c)){
            for(j=k; j>=0; j--){
                var d = s.charAt(j);
                if(t.contains(""+d)){
                    r+=d;
                    k=j-1;
                    break;
                }            
            }
        }else{
            r+=c;
        }
    }
    return r;
}
```

##### 스택과 큐를 벗어나 이중포문이긴 하지만 O(n)인 코드
```java
String reverseVowelsOfString(String s) {
    int i,j,k,l=s.length();
    k = l-1;
    var r="";
    for(i=0; i<l; i++){
        var c = s.charAt(i);
        if("aeiouAEIOU".contains(""+c)){
            for(j=k; j>=0; j--){
                var d = s.charAt(j);
                if("aeiouAEOIU".contains(""+d)){
                    r+=d;
                    k=j-1;
                    break;
                }            
            }
        }else{
            r+=c;
        }
    }
    return r;
}
```

##### 파이썬도 마찬가지
```python
def reverseVowelsOfString(s):
    a=[]
    b=[]
    c=[]
    for k in s:
        if k in 'aeiouAEIOU':
            a.append(k)
            c.append(0)
        else:
            b.append(k)
            c.append(1)
    r=''
    for d in c:
        if d is 0:
            r+=a.pop(-1)
        else:
            r+=b.pop(0)
    return r
```

```python
def reverseVowelsOfString(s):
    t = 'aeiouAEIOU'
    r = ''
    l = list(s)
    for a in s:
        if a in t:
            for b in l[::-1]:
                del l[-1]
                if b in t:
                    r+=b
                    break
        else:
            r+=a
    
    return r
```