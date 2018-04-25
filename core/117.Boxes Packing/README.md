You are given n rectangular boxes, the ith box has the length lengthi, the width widthi and the height heighti. Your task is to check if it is possible to pack all boxes into one so that inside each box there is no more than one another box (which, in turn, can contain at most one another box, and so on). More formally, your task is to check whether there is such sequence of n different numbers pi (1 ≤ pi ≤ n) that for each 1 ≤ i < n the box number pi can be put into the box number pi+1.
A box can be put into another box if all sides of the first one are less than the respective ones of the second one. You can rotate each box as you wish, i.e. you can swap its length, width and height if necessary.
Example
For length = [1, 3, 2], width = [1, 3, 2] and height = [1, 3, 2], the output should be
boxesPacking(length, width, height) = true;
For length = [1, 1], width = [1, 1] and height = [1, 1], the output should be
boxesPacking(length, width, height) = false;
For length = [3, 1, 2], width = [3, 1, 2] and height = [3, 2, 1], the output should be
boxesPacking(length, width, height) = false.

```java
boolean boxesPacking(int[] length, int[] width, int[] height) {
    
    int newBox[][] = new int[length.length][3];
    
    for(int i=0; i<length.length; i++){
        newBox[i][0] = width[i];
        newBox[i][1] = height[i];
        newBox[i][2] = length[i];
        Arrays.sort(newBox[i]);
    }
    
    for(int j=0; j<length.length-1; j++){
        for(int k=j+1; k<length.length; k++){
            if(!(newBox[j][0]>newBox[k][0] && newBox[j][1]>newBox[k][1] && newBox[j][2]>newBox[k][2]) && !(newBox[j][0]<newBox[k][0] && newBox[j][1]<newBox[k][1] && newBox[j][2]<newBox[k][2])){
            return false;
            }
        }        
    }    
    return true;
}
```