In order to stop the Mad Coder evil genius you need to decipher the encrypted message he sent to his minions. The message contains several numbers that, when typed into a supercomputer, will launch a missile into the sky blocking out the sun, and making all the people on Earth grumpy and sad.
You figured out that some numbers have a modified single digit in their binary representation. More specifically, in the given number n the kth bit from the right was initially set to 0, but its current value might be different. It's now up to you to write a function that will change the kth bit of n back to 0.
Example
For n = 37 and k = 3, the output should be
killKthBit(n, k) = 33.
37 = 100101 ~> 100001 = 33.
For n = 37 and k = 4, the output should be
killKthBit(n, k) = 37.
The 4th bit is 0 already (looks like the Mad Coder forgot to encrypt this number), so the answer is still 37.


```java
int killKthBit(int n, int k) {
  /**
  * 37의 경우 2진법으로 나타내면 100101이고 2의 2승 자리에 1이 있는지 없는지를 알려면 2를 두번 나눈 몫인 9를 2로 한번 더 나눠
  *그 나머지 값이 1인지 아닌지를 판별하면 된다.
  **/
  return n/(int)Math.pow(2,k-1)%2==1?n-(int)Math.pow(2,k-1):n ;
}
```

##### 고수의 풀이
```java
int killKthBit(int n, int k) {
  return n & (~(1<<k-1)) ;
}
```
