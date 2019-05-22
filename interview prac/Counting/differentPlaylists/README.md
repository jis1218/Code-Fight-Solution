Sam likes to listen to music while he travels. His MP3 player contains n songs and he wants to listen to l songs during a trip. He likes hearing songs again, so these l songs don't necessarily have to be different. He has created a playlist such that a song can be played again only if at least k other songs have already been played.

Sam wants to know how many different playlists he could possibly create. Can you help Sam determine this number? As this number can be very large, return the number modulo 109 + 7.

Example

For n = 5, k = 3, and l = 6, the output should be
differentPlaylists(n, k, l) = 480.

The first song can be any of the 5.
The second song can be any except the first song played, so the number of variants for second song is 4.
The third song can be any except the first and the second played, so the number of variants for it is 3.
The fourth song can be any except the first three played, so the number of variants for it is 2.
The fifth song can be equal to the song that was played first, because 3 other songs have now been played. But it can't be equal to the second to the fourth songs, so the number of variants is 2.
For the sixth song we can choose from the first two songs played, but it can't be one of the third to the fifth songs, so again the number of variants is 2.
Thus, the answer is 5 * 4 * 3 * 2 * 2 * 2 = 480.

##### 결국 nPk * (n-k)^(l-k)를 하는 문제인데
##### 어려웠던 부분은 (n-k)^(l-k)를 하는 부분이다.
##### 일일이 제곱을 하면 시간이 많이 걸려서 Time Exception이 뜬다.
##### 따라서 이를 어떻게 풀지가 중요한데
##### 예를들어 2^13인 경우 13은 2진법으로 1011로 나타낼 수 있으므로 2^3 * 2^1 * 2^0으로 나타낼 수 있다.
##### 아래 pow 함수가 그 부분이다.

```java
int mod = (int)Math.pow(10,9)+7;
int differentPlaylists(int n, int k, int l) {
    long sum = 1;
    int temp = n;
    for(int i = 0; i<Math.min(k, l); i++){
        sum *= n;        
        sum %= mod;                 
        n = n-1;
    }
    int a = l-k<0?0:l-k;
    return (int)((sum * (pow(n, a)%mod)) % mod);

}

long pow(int n, int p){
    long result = 1;
    long temp = n;
    while(p>0){
        if(p%2==1) result = (result * temp) % mod;
        temp = (temp*temp) % mod;
        p/=2;  
    }
    return result; 
}
```