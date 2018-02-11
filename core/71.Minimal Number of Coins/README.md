You find yourself in Bananaland trying to buy a banana. You are super rich so you have an unlimited supply of banana-coins, but you are trying to use as few coins as possible.
The coin values available in Bananaland are stored in a sorted array coins. coins[0] = 1, and for each i (0 &lt; i &lt; coins.length) coins[i] is divisible by coins[i - 1]. Find the minimal number of banana-coins you'll have to spend to buy a banana given the banana's price.
Example
For coins = [1, 2, 10] and price = 28, the output should be
minimalNumberOfCoins(coins, price) = 6.
```java
int minimalNumberOfCoins(int[] coins, int price) {
    int num = coins.length-1;
    int sum=0;
    while(num>=0){        
        sum += price/coins[num];
        price %= coins[num];
        num--;
    }    
    return sum;
}
```