You are given an array of integers that you want distribute between several groups. The first group should contain numbers from 1 to 104, the second should contain those from 104 + 1 to 2 * 104, ..., the 100th one should contain numbers from 99 * 104 + 1 to 106 and so on.
All the numbers will then be written down in groups to the text file in such a way that:
the groups go one after another;
each non-empty group has a header which occupies one line;
each number in a group occupies one line.
Calculate how many lines the resulting text file will have.
Example
For a = [20000, 239, 10001, 999999, 10000, 20566, 29999], the output should be
numbersGrouping(a) = 11.
```java
int numbersGrouping(int[] a) {
    int b[] = new int[(int)Math.pow(10,5)];
    int sum=0;
    
    for(int i : a){
        if(b[(i-1)/10000]==0){
            b[(i-1)/10000]++;
            sum++;
        }
    }    
    return sum +a.length;

}
```