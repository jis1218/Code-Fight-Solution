
##### 난이도는 쉬움인데 엄청 오래걸렸다. 그리고 코드도 마음에 안든다. 
```java
String minSubstringWithAllChars(String s, String t) {
    
    if(t.length()==0) return "";
    
    char[] res = new char[26];
    int result = s.length();
    String resu = s;
    for(int i=0; i<s.length(); i++){
        int min = s.length();
        int index = i;
        if(t.contains(String.valueOf(s.charAt(i)))){
            boolean flag = false;
            
            for(int j=i; j<s.length(); j++){
                if(t.contains(String.valueOf(s.charAt(j)))){
                    System.out.println("i = " + i + ", j = " + j);
                    res[s.charAt(j)-'a']++;                
                    for(int k=0; k<t.length(); k++){
                        if(res[t.charAt(k)-'a']>=1){
                            flag = true;
                        }else{
                            flag = false;
                            break;
                        }
                    }
                    if(flag){
                        min = j-i;
                        index = j;
                        res = new char[26];
                        System.out.println(min);
                        break;
                    }
                }
            }
        }
        if(result>min){
            result = min;
            resu = s.substring(i, index+1);
        }
        
    }
    
    return resu;
                                                     
}
```

#####
```python
def minSubstringWithAllChars(s, t):
    for x in range(len(s)+1):
        for p in range(len(s)-x+1):
            c = filter(lambda x: x in t,s[p:p+x])
            if len(set(c))==len(t):
                return s[p:p+x]
    return ""
```

##### 아래 코드를 실행해봤는데 만약에 ''.join(c)를 해버리면 c가 소모가 되버리는 것 같다. 그래서 밑에 list(c)에 아무것도 안찍힌다.
```python
if __name__ == '__main__':
    
    def minSubstringWithAllChars(s, t):
        flag = False
        for x in range(len(s)+1):
            for p in range(len(s)-x+1):
                c = filter(lambda x: x in t,s[p:p+x])
                print(''.join(c) + ', '+s[p:p+x])
                print(list(c))
                if len(set(c))==len(t):
                    return s[p:p+x]
        return ""
    
    a = minSubstringWithAllChars('adobecodebanc', 'abc')
    print(a)
    print('what the')
```