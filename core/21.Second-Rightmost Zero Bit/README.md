Presented with the integer n, find the 0-based position of the second rightmost zero bit in its binary representation (it is guaranteed that such a bit exists), counting from right to left.
Return the value of 2position_of_the_found_bit.
Example
For n = 37, the output should be
secondRightmostZeroBit(n) = 8.
37 = 100101. The second rightmost zero bit is at position 3 (0-based) from the right in the binary representation of n.
Thus, the answer is 23 = 8.


##### 예를 들어 37이 100101이라 할때 ~37은 1111....011010이고 여기서 lowestOneBit을 하면 2가 나오는데 2를 이진법으로 하면 10이다.
##### 1111....011010과 10을 XOR 연산자로 계산해주면 1111....011000이 되고 이 수의 lowestOneBit을 하면 두번째의 rightmost zero값을 알 수가 있다.
```java
int secondRightmostZeroBit(int n) {
  return Integer.lowestOneBit(Integer.lowestOneBit(~n)^~n);
}
```

##### 이런 풀이도 있다.
```java
int secondRightmostZeroBit(int n) {
  return ~(n|(n+1)) & ((n|(n+1))+1) ;
}
```
