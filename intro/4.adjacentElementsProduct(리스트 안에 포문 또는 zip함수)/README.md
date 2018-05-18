Given an array of integers, find the pair of adjacent elements that has the largest product and return that product.
Example
For inputArray = [3, 6, -2, -5, 7, 3], the output should be
adjacentElementsProduct(inputArray) = 21.
7 and 3 produce the largest product.
```python
def adjacentElementsProduct(inputArray):
    return max([inputArray[i]*inputArray[i+1] for i in range(len(inputArray)-1)])
```

##### 이런 풀이도 있네 - zip 함수... 하나로 묶어준다.
```python
def adjacentElementsProduct(inputArray):
    return max(a * b for a, b in zip(inputArray[:-1], inputArray[1:]))
```

```java
int adjacentElementsProduct(int[] inputArray) {
    
    int max = inputArray[0]*inputArray[1];
    
    for(int i=0; i<inputArray.length-1; i++){
        
        if(max<inputArray[i]*inputArray[i+1]){
            max = inputArray[i]*inputArray[i+1];
        }
        
    }
    
    return max;

}
```