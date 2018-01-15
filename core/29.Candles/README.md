When a candle finishes burning it leaves a leftover. makeNew leftovers can be combined to make a new candle, which, when burning down, will in turn leave another leftover.
You have candlesNumber candles in your possession. What's the total number of candles you can burn, assuming that you create new candles as soon as you have enough leftovers?
Example
For candlesNumber = 5 and makeNew = 2, the output should be
candles(candlesNumber, makeNew) = 9.
Here is what you can do to burn 9 candles:
burn 5 candles, obtain 5 leftovers;
create 2 more candles, using 4 leftovers (1 leftover remains);
burn 2 candles, end up with 3 leftovers;
create another candle using 2 leftovers (1 leftover remains);
burn the created candle, which gives another leftover (2 leftovers in total);
create a candle from the remaining leftovers;
burn the last candle.
Thus, you can burn 5 + 2 + 1 + 1 = 9 candles, which is the answer.
```java
int candles(int candlesNumber, int makeNew) {

    int sum = candlesNumber;

    while(true){
        sum += candlesNumber/makeNew;
        candlesNumber = candlesNumber/makeNew + candlesNumber%makeNew;
        if(candlesNumber<makeNew) break;
    }
    return sum;
}
```

##### 다른 풀이
```java
int candles(int candlesNumber, int makeNew) {

	 return (int) (candlesNumber + Math.floor((candlesNumber - 1) / (makeNew - 1)));
	 }
```
