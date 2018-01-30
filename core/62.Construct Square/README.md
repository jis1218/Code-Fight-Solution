Given a string consisting of lowercase English letters, find the largest square number which can be obtained by reordering the string's characters and replacing them with any digits you need (leading zeros are not allowed) where same characters always map to the same digits and different characters always map to different digits.
If there is no solution, return -1.
Example
For s = "ab", the output should be
constructSquare(s) = 81.
The largest 2-digit square number with different digits is 81.
For s = "zzz", the output should be
constructSquare(s) = -1.
There are no 3-digit square numbers with identical digits.
For s = "aba", the output should be
constructSquare(s) = 900.
It can be obtained after reordering the initial string into "baa" and replacing "a" with 0 and "b" with 9.

##### 고생고생해서 푼 풀이...

```java
int constructSquare(String s) {
    int num = 9;
    String bb = s;
    for(int i=0; i<s.length(); i++){
        if(bb.charAt(i)>='a' && bb.charAt(i)<='z'){
           bb = bb.replace(""+bb.charAt(i), ""+num);
            num--;
            System.out.println(bb);
        }       
    }    
    int fin = Integer.valueOf(bb);
    int max = (int) Math.sqrt(Math.pow(10, s.length()));
    int min = (int) Math.ceil(Math.sqrt(Math.pow(10, s.length()-1)));
    
    for(int i=max; i>=min; i--){
        int com = (int) Math.pow(i, 2);

            if(Arrays.equals(checkNum(fin), checkNum(com))){
                return com;
            }   
    }    
    return -1;
}
int[] checkNum(int a){
    int[] res = new int[10];
    
    while(true){
        res[a%10]++;
        a /= 10;        
        if(a==0) break;
    }
    Arrays.sort(res);
    return res;
}
```
##### 다른 사람의 풀이 (컨셉은 비슷해 보인다)
```java
int constructSquare(String s) {
    int[] list = new int[26];
    for (byte b : s.getBytes())
        list[b - 'a']++;
    Arrays.sort(list);
    
    int best = -1;
    for (int i = 1; i < 10000; i++) {
        int[] count = new int[26];
        long j = i*i;
        while (j > 0) {
            count[(int)(j%10)]++;
            j/=10;
        }
        Arrays.sort(count);
        if (Arrays.equals(count, list))
            best = i*i;
    }
    return best;
}
```
