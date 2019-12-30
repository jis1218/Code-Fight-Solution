```java
String classifyStrings(String s) {

    int vowel = 0;
    int constant = 0;
    int question = 0;
    boolean flagVowel = false;
    boolean flagCons = false;
    boolean flag1 = false;
    boolean flag2 = false;
    boolean flag3 = false;

    for(int i=0; i<s.length(); i++){
        if(isVowels(s.charAt(i))){
            vowel++;
            constant = 0;
            flagCons = false;
            question=0;
        }else if(s.charAt(i)=='?'){
            flagVowel = true;
            flagCons = true;
            vowel++;
            constant++;
            question++;
        }else{
            constant++;
            vowel = 0;
            flagVowel = false;
            question=0;
        }
        
        if((vowel==3 && !flagVowel)||(constant==5 && !flagCons)) return "bad";
        if(vowel==3 && flagVowel) flag1 = true;
        if(constant==5 && flagCons) flag2 = true;
        if((flag1 || flag2) && question==1) flag3 = true;
    }
    if(flag1 && flag2 && flag3) return "bad";
    else if(flag1 || flag2) return "mixed";
    return "good";
}

boolean isVowels(char c){
    if(c=='a' || c=='e' || c=='i' || c=='o' || c=='u') return true;
    return false;
}
```

##### 정규식으로 끝낸 깔끔한 풀이
```java
String classifyStrings(String s) {
    if(s.matches(".*([aeiou]{3}|[bcdfghjklmnpqrstvwxyz]{5}).*"))
        return "bad";
    if(s.matches(".*([aeiou?]{3}|[bcdfghjklmnpqrstvwxyz?]{5}).*"))
        return "mixed";
    return "good";
}
```