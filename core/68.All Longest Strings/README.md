Given an array of strings, return another array containing all of its longest strings.
Example
For inputArray = ["aba", "aa", "ad", "vcd", "aba"], the output should be
allLongestStrings(inputArray) = ["aba", "vcd", "aba"].
```java
String[] allLongestStrings(String[] inputArray) {
    ArrayList<String> list = new ArrayList<>();
    int maxLen = 0;
    for(String s : inputArray){
        if(maxLen < s.length()){
            maxLen = s.length();
            list.clear();
        }
        
        if(maxLen==s.length()){
            list.add(s);
        }
    }
    
    String str[] = new String[list.size()];
    
    return list.toArray(str);

}
```