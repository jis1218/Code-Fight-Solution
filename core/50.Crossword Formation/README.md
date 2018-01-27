You're a crossword fanatic, and have finally decided to try and create your own. However, you also love symmetry and good design, so you come up with a set of rules they should follow:
the crossword must contain exactly four words;
these four words should form four pairwise intersections;
all words must be written either left-to-right or top-to-bottom;
the area of the rectangle formed by empty cells inside the intersections isn't equal to zero.
Given 4 words, find the number of ways to make a crossword following the above-described rules. Note that two crosswords which differ by rotation are considered different.
Example
For words = ["crossword", "square", "formation", "something"], the output should be
crosswordFormation(words) = 6.

##### 최종 풀이... 처음에 words[0]이 첫번째, 두번째 오는 경우의 수만 생각하였음
##### 결국 세번째, 네번째 오는 경우의 수를 빠뜨렸다는 것을 알고 수정 완료

int crosswordFormation(String[] words) {
    int a1, a2, a3, a4, a5, a6, a7, a8;
    int[][] order = {
        {1, 2, 3}, {1, 3, 2}, {2, 1, 3}, {2, 3, 1}, {3, 1, 2}, {3, 2, 1}
    };
    
    int result = 0;
    String a;
    String b;
    String c;
    String d;
    for(int t=0; t<2; t++){        
        for(int aa=0; aa<6; aa++){
            if(t==0){
                a=words[0];
                b=words[order[aa][0]];
                c=words[order[aa][1]];
                d=words[order[aa][2]];
            }else{
                a=words[order[aa][0]];
                b=words[order[aa][1]];
                c=words[0];
                d=words[order[aa][2]];                
            }        
        
        for(int i=0; i<a.length()-2; i++){
            for(int j=0; j<b.length()-2; j++){
                if(a.charAt(i)==b.charAt(j)){
                    a1 = i;
                    a2 = j;                
                    for(int k=a2+2; k<b.length(); k++){
                        for(int l=0; l<c.length()-2; l++){
                            if(b.charAt(k)==c.charAt(l)){
                                a3 = k;
                                a4 = l;
                                for(int m=a4+2; m<c.length(); m++){
                                    for(int n=d.length()-1; n>=2; n--){
                                        if(c.charAt(m)==d.charAt(n)){
                                            a5 = m;
                                            a6 = n;
                                            for(int p=a6-2; p>=0; p--){
                                                for(int q=a1+2; q<a.length(); q++){ 
                                                    if(d.charAt(p)==a.charAt(q)){
                                                        a7 = p;
                                                        a8 = q;
                                                        if(a3-a2==a6-a7 && a8-a1==a5-a4){
                                                            result++;
                                                            
                                                        }
                                                    }
                                                }
                                            }
                                        }
                                    }
                                }
                            }
                        }
                    }
                }
            }
        }
    }
    }
    return result*2;
}


##### 다른 풀이
```java
int crosswordFormation(String[] words) {
    int t = 0;
    for (int i = 0; i < words.length; i++)
        for (int j = 0; j < words.length; j++)
            for (int k = 0; k < words.length; k++)
                for (int l = 0; l < words.length; l++)
                    if (i != j && i != k && i != l && 
                        j != k && j != l && k != l)
                        t+=check(words[i],words[j],words[k],words[l]);
    return t;
}

int check (String a, String b, String c, String d) {
    int t = 0;
    for (int a1 = 0; a1 < a.length(); a1++)
    for (int a2 = a1+2; a2 < a.length(); a2++)
    for (int b1 = 0; b1 < b.length(); b1++)
    for (int b2 = b1+2; b2 < b.length(); b2++)
    for (int c1 = 0; c1 < c.length(); c1++)
    for (int d1 = 0; d1 < d.length(); d1++) {
        int c2 = c1 + (a2-a1);
        int d2 = d1 + (b2-b1);
        if (c2 < c.length() && d2 < d.length()) {
            if (a.charAt(a1)==b.charAt(b1)
               && a.charAt(a2)==d.charAt(d1)
               && c.charAt(c1)==b.charAt(b2)
               && c.charAt(c2)==d.charAt(d2))
                t++;
        }
    }
    return t;
    ```