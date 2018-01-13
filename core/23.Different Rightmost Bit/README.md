You're given two integers, n and m. Find position of the rightmost bit in which they differ in their binary representations (it is guaranteed that such a bit exists), counting from right to left.
Return the value of 2position_of_the_found_bit (0-based).
Example
For n = 11 and m = 13, the output should be
differentRightmostBit(n, m) = 2.
11 = 1011, 13 = 1101, the rightmost bit in which they differ is the bit at position 1 (0-based) from the right in the binary representations.
So the answer is 2.
For n = 7 and m = 23, the output should be
differentRightmostBit(n, m) = 16.
7 = 111, 23 = 10111, i.e.
00111
10111
So the answer is 16.
##### 나의 풀이
```java
int differentRightmostBit(int n, int m) {
  return Integer.lowestOneBit(n^m) ;
}
```
##### 다른 풀이 - 자기 자신과 그 음수의 & 연산을 하면 lowestOneBit이 나오게 된다.
```java
int differentRightmostBit(int n, int m) {
  return (n^=m) & -n ;
}
```
