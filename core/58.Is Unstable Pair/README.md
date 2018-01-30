Some file managers sort filenames taking into account case of the letters, others compare strings as if all of the letters are of the same case. That may lead to different ways of filename ordering.
Call two filenames an unstable pair if their ordering depends on the case.
To compare two filenames a and b, find the first position i at which a[i] ≠ b[i]. If a[i] < b[i], then a < b. Otherwise a > b. If such position doesn't exist, the shorter string goes first.
Given two filenames, check whether they form an unstable pair.
Example
For filename1 = "aa" and filename2 = "AAB", the output should be
isUnstablePair(filename1, filename2) = true.
Because "AAB" < "aa", but "AAB" > "AA".
For filename1 = "A" and filename2 = "z", the output should be
isUnstablePair(filename1, filename2) = false.
Both "A" < "z" and "a" < "z".

```java
boolean isUnstablePair(String filename1, String filename2) {
    String[] str = new String[2];
    String[] ref = new String[2];
    str[0]=filename1;
    str[1]=filename2;
    Arrays.sort(str);
    
    ref[0]=filename1.toLowerCase();
    ref[1]=filename2.toLowerCase();
    Arrays.sort(ref);    
    
    return !str[0].toLowerCase().equals(ref[0]); 
}
```

##### 고수의 풀이
```java
boolean isUnstablePair(String filename1, String filename2) {
    return (filename1.compareTo(filename2) * 
           ((filename1.toLowerCase()).compareTo(filename2.toLowerCase())) < 0);
}
```