You are given an array of up to four non-negative integers, each less than 256.
Your task is to pack these integers into one number M in the following way:
The first element of the array occupies the first 8 bits of M;
The second element occupies next 8 bits, and so on.
Return the obtained integer M.
Note: the phrase "first bits of M" refers to the least significant bits of M - the right-most bits of an integer. For further clarification see the following example.
Example
For a = [24, 85, 0], the output should be
arrayPacking(a) = 21784.
An array [24, 85, 0] looks like [00011000, 01010101, 00000000] in binary.
After packing these into one number we get 00000000 01010101 00011000 (spaces are placed for convenience), which equals to 21784.
```java
int arrayPacking(int[] a) {

    int sum = 0;

    for(int i=0; i<a.length; i++){
        sum += a[i] * (int) Math.pow(2, 8*i);
    }

    return sum;

}
```
##### 다른 풀이
```java
int arrayPacking(int[] a) {
    int n = 0;
    for(int i = a.length-1; i >= 0; i--) {
        n <<= 8; //n = n<<8
        n += a[i];
    }
    // 첫번째 for 문 후 -> 00000000 00000000
    // 두번째 for 문 후 -> 00000000 00000000 01010101
    // 세번째 for 문 후 -> 00000000 00000000 01010101 00011000
    return n;
}
```

##### 자바 시프트 연산자
○ 왼쪽 시프트 연산자 <<
178 << 2 : 178 의 이진코드를 왼쪽으로 2비트 시프트 한다.
  10110010
1011001000
왼쪽으로 두칸 밀면서, 비게 되는 오른쪽 두칸은 0 으로 채운다.
그런데, 문제는 왼쪽으로 밀면서 기존의 크기를 넘어서기 때문에 왼쪽으로 넘어선 2개의 비트는 삭제된다.
따라서, 10110010 을 왼쪽으로 밀면 왼쪽 두개 비트인 10 은 삭제되고, 오른쪽의 2개 비트는 0으로 채워져
결과값은 11001000 이 된다.
출처:[java] 비트 연산자와 시프트 연산자

○ 오른쪽 시프트 연산자 >>
178 >> 2 : 178의 이진코드를 오른쪽으로 2 비트 시프트 한다.
10110010
1110110010
오른쪽으로 2비트 이동한후, 비게되는 왼쪽의 2개비트는 1로 채워지고, 오른쪽에서 2비트 넘어간 부분은 삭제된다.
따라서, 10110010 을 오른쪽으로 2비트 시프트하면, 11101100 이 된다.
그런데, 주의할점은, 오른쪽으로 밀면서 왼쪽에 비게되는 비트부분이 무조건 1 로 채워지는 것이 아니라,
밀기전의 최초 첫째자리 값과 동일한 값으로 채워진다는 것이다.
여기에서는 밀기전의 첫째자리값이 1 이었으므로, 1 로 채워진 것이다.
출처:[java] 비트 연산자와 시프트 연산자

○ 논리 오른쪽 시프트 연산자 >>>
178 >>> 2 : 오른쪽으로 2 비트 시프트한다.
자바에 추가된 논리 시프트는 오른쪽으로 밀면서 비게되는 앞쪽 비트를 무조건 0 으로 채워넣는 것이다.
10110010
0010110010
으로 되는 것으로,
역시 오른쪽으로 밀려난 2개 비트 10 은 삭제되고, 비게되는 왼쪽 2비트는 무조건 0으로 채워진다.
따라서 10110010 을 오른쪽으로 논리 시프트 하면, 00101100 이 된다.
출처:[java] 비트 연산자와 시프트 연산자
