You're given two integers, n and m. Find position of the rightmost pair of equal bits in their binary representations (it is guaranteed that such a pair exists), counting from right to left.
Return the value of 2position_of_the_found_pair (0-based).
Example
For n = 10 and m = 11, the output should be
equalPairOfBits(n, m) = 2.
1010 = 10102, 1110 = 10112, the position of the rightmost pair of equal bits is the bit at position 1 (0-based) from the right in the binary representations.
So the answer is 21 = 2.
##### 나의 풀이 - n^m을 하면 공통인것만 0이 되고 여기에 ~를 붙이면 공통인 것만 1이 된다. 여기에 -를 붙인 값과 & 연산을 해주면 가장 오른쪽의 1의 값을 얻을 수 있다.
```java
int equalPairOfBits(int n, int m) {
  return ~(n^=m)&-~n ;
}
```
