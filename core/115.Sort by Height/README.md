Some people are standing in a row in a park. There are trees between them which cannot be moved. Your task is to rearrange the people by their heights in a non-descending order without moving the trees.
Example
For a = [-1, 150, 190, 170, -1, -1, 160, 180], the output should be
sortByHeight(a) = [-1, 150, 160, 170, -1, -1, 180, 190]
```java
int[] sortByHeight(int[] a) {
    for(int i=0; i<a.length; i++){
        if(a[i]!=-1){
            for(int j=i; j<a.length; j++){
                if(a[j]!=-1 && a[i]>a[j]){
                    int temp = a[i];
                    a[i]=a[j];
                    a[j]=temp;
                }
            }
        }        
    }
    return a;
}
```