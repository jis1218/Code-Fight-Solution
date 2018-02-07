Two arrays are called similar if one can be obtained from another by swapping at most one pair of elements in one of the arrays.
Given two arrays a and b, check whether they are similar.
```java
boolean areSimilar(int[] a, int[] b) {
    
    int count = 0;
    for(int i=0; i<a.length; i++){
        if(a[i]!=b[i]) count++;
    }
    
    Arrays.sort(a);
    Arrays.sort(b);
    
    if(!Arrays.equals(a,b)) return false;
    if(count>2) return false;
    
    return true;
}
```