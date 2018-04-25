Given an array of strings, sort them in the order of increasing lengths. If two strings have the same length, their relative order must be the same as in the initial array.

##### 나의 풀이
```java
String[] sortByLength(String[] inputArray) {
    for(int i=0; i<inputArray.length-1; i++){
        for(int j=i+1; j<inputArray.length; j++){
            if(inputArray[i].length()>inputArray[j].length()){
                String temp = inputArray[i];
                inputArray[i] = inputArray[j];
                inputArray[j] = temp;
            }
        }
    }
    return inputArray;

}
```

##### 이런 방법도 있다네
```java
String[] sortByLength(String[] inputArray) {

    Arrays.sort(inputArray, new Comparator<String>(){
        public int compare(String o1, String o2) {
            if (o1.length() > o2.length()) {
                return 1;
            } else if (o1.length() < o2.length()) {
                return -1;
            } else {
                return 0;
            }
        }
    });
    
    return inputArray;
}
```
##### 위를 람다식으로 쓰면
```java
String[] sortByLength(String[] inputArray) {
    Arrays.sort(inputArray, (o1, o2) -> Integer.compare(o1.length(), o2.length()));
    return inputArray;
}
```