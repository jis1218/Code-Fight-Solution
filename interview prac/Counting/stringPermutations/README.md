Given a string s, find all its potential permutations. The output should be sorted in lexicographical order.

Example

For s = "CBA", the output should be
stringPermutations(s) = ["ABC", "ACB", "BAC", "BCA", "CAB", "CBA"];
For s = "ABA", the output should be
stringPermutations(s) = ["AAB", "ABA", "BAA"].

##### 이제 permutation, combination은 나만의 코드로 완성 가능

```java
String[] stringPermutations(String s) {
    helper(s, new String(""), s.length());
    String[] result =  set.toArray(new String[0]);
    Arrays.sort(result);
    return result;

}

HashSet<String> set = new HashSet<>();

void helper(String s, String result, int len){
    if(result.length()==len){
        set.add(result);
    }
    for(int i=0; i<s.length(); i++){
        result += String.valueOf(s.charAt(i));
        helper(s.substring(0, i) + s.substring(i+1, s.length()), result, len);
        result = result.substring(0, result.length()-1);        
    }
}
```