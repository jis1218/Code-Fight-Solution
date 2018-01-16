Consider a sequence of numbers a0, a1, ..., an, in which an element is equal to the sum of squared digits of the previous element. The sequence ends once an element that has already been in the sequence appears again.
Given the first element a0, find the length of the sequence.

```java
int squareDigitsSequence(int a0) {
    ArrayList<Integer> list = new ArrayList<>();
    boolean flag = false;
    int ori = a0;
    while(true){
        int sum = 0;
        list.add(ori);

        while(ori>0){
            sum += (ori%10)*(ori%10);
            ori /= 10;
        }

        ori = sum;

        for(int i = 0; i<list.size(); i++){
            if(sum==list.get(i)){
                flag = true;
            }
        }

        if(flag) break;
    }

    return list.size()+1;

}
```
