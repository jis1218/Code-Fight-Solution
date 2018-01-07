
Reverse the order of the bits in a given integer.
Example
For a = 97, the output should be
mirrorBits(a) = 67.
97 equals to 1100001 in binary, which is 1000011 after mirroring, and that is 67 in base 10.
For a = 8, the output should be
mirrorBits(a) = 1.
```java
int mirrorBits(int a) {

    int b = Integer.reverse(a);

    return b>>>(32-Integer.toBinaryString(a).length());
}
```

##### 다른 풀이1
```java
int mirrorBits(int a) {
int b = 0;
  while (a > 0) {
    b <<= 1;
    b |= a & 1;
    a >>= 1;
  }

  return b;
}
```
##### 다른 풀이2
```java
int mirrorBits(int a) {
    int b = 0;
    while (a > 0) {
        b *= 2;
        b += a%2;
        a /= 2;
    }
    return b;
}
```
