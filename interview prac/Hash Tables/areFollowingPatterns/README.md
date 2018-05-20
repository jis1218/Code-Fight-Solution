Given an array strings, determine whether it follows the sequence given in the patterns array. In other words, there should be no i and j for which strings[i] = strings[j] and patterns[i] ≠ patterns[j] or for which strings[i] ≠ strings[j] and patterns[i] = patterns[j].
Example
For strings = ["cat", "dog", "dog"] and patterns = ["a", "b", "b"], the output should be
areFollowingPatterns(strings, patterns) = true;
For strings = ["cat", "dog", "doggy"] and patterns = ["a", "b", "b"], the output should be
areFollowingPatterns(strings, patterns) = false.
```java
boolean areFollowingPatterns(String[] strings, String[] patterns) {
    Hashtable<String, String> table = new Hashtable<>();
    HashSet<String> set = new HashSet<>();
    for(int i=0; i<strings.length; i++){
        if(table.get(strings[i])==null){
            table.put(strings[i], patterns[i]);
            set.add(patterns[i]);
        }else{
            if(!table.get(strings[i]).equals(patterns[i])){
                return false;
            }
        }        
    }    
    return table.size()==set.size();
}
```