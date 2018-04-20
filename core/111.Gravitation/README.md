You are given a vertical box divided into equal columns. Someone dropped several stones from its top through the columns. Stones are falling straight down at a constant speed (equal for all stones) while possible (i.e. while they haven't reached the ground or they are not blocked by another motionless stone). Given the state of the box at some moment in time, find out which columns become motionless first.
Example
For
rows = ["#..##",
        ".##.#",
        ".#.##",
        "....."]
the output should be gravitation(rows) = [1, 4].

```java
int[] gravitation(String[] rows) {
    int value[] = new int[rows[0].length()];
    int min = rows.length;
    int total = 0;
    int subtotal = 0;
    
    for(int i=0; i<rows[0].length(); i++){
        int cnt=0;
        int mcnt=0;
        boolean flag=true;
        for(int j=rows.length-1; j>=0; j--){
            if(rows[j].charAt(i)!='#'){
                cnt++;
            }
        }
        
        for(int k=0; k<rows.length; k++){
            if(rows[k].charAt(i) == '.'){
                mcnt++;
            }else{
                flag = false;
                break;
            }
            
        }
        if(flag){
            mcnt=0;
        }
        value[i]=cnt-mcnt;
        if(min>value[i]){
            min = value[i];
            total = 1;
        }else if(min==value[i]){
            total++;
        }else if(value[i]==rows.length){
            subtotal++;
        }
        System.out.println(value[i]);
    }
    
    int result[] = new int[total+subtotal];
    int count = 0;
    for(int i=0; i<value.length; i++){
        if(value[i]==min || value[i]==rows.length){
            result[count]=i;
            count++;
        }
    }
    
    return result;
}
```

##### 다른 풀이
```java
int[] gravitation(String[] rows) {
    int[] time = new int[rows[0].length()];
    int[] top = new int[rows[0].length()];
    Arrays.fill(top,-1);
    for (int i = 0; i < rows.length; i++) {
        for (int j = 0; j < rows[i].length(); j++) {
            if (rows[i].charAt(j) == '#' && top[j] < 0)
                top[j] = j;
            if (rows[i].charAt(j) == '.' && top[j] >= 0)
                time[j] ++;
        }
    }
    int min = time[0];
    int count = 0;
    for (int i : time) {
        if (i < min) {
            min = i;
            count = 0;
        }
        if (i == min)
            count++;
    }
    int[] result = new int[count];
    int j = 0;
    for (int i = 0; i < time.length; i++)
        if (time[i] == min)
            result[j++] = i;
    
    return result;
    
}
