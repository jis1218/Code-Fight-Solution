Note: Write a solution with O(n) time complexity and O(1) additional space complexity, since this is what you would be asked to do during a real interview.
Given an array a that contains only numbers in the range from 1 to a.length, find the first duplicate number for which the second occurrence has the minimal index. In other words, if there are more than 1 duplicated numbers, return the number for which the second occurrence has a smaller index than the second occurrence of the other number does. If there are no such elements, return -1.
Example
For a = [2, 3, 3, 1, 5, 2], the output should be
firstDuplicate(a) = 3.
There are 2 duplicates: numbers 2 and 3. The second occurrence of 3 has a smaller index than than second occurrence of 2 does, so the answer is 3.
For a = [2, 4, 3, 5, 1], the output should be
firstDuplicate(a) = -1.
##### 최종 풀이
```java
int firstDuplicate(int[] a) {

    int b[]=Arrays.copyOf(a, a.length);
    Arrays.sort(b);
    int index = a.length;

    for(int i=0; i<b.length-1; i++){
        if(b[i]==b[i+1]){
            int num=0;
            for(int j=0; j<a.length; j++){

                if(b[i]==a[j]){
                    if(num==1 && j<index){
                    index = j;
                    break;
                }
                    num++;
                }

            }

        }
    }

    return index==a.length?-1:a[index];
}
```

##### 첫번째 풀이로 하면 a 배열의 길이가 길어질 경우 시간이 엄청 걸린다. O(N의 제곱) 만큼 시간이 걸린다.
```java
int index = a.length;
		for(int i=0; i<a.length-1; i++){
			for(int j=i+1; j<a.length; j++){
				if(a[i]==a[j]){
					if(j<index){
						index = j;
						break;
					}
				}
			}
		}
    return index==a.length?-1:a[index];
  }
```

##### 고수의 풀이 - Negation을 이용하라! 반복되는 수는 같은 곳을 바라본다. 즉 처음에 2가 나와 a[2-1]의 수를 음수로 바꾸었다면 다음 나오는 2는 음수를 가리키므로 결국 반복되는 위치를 찾을 수가 있다.
```java
int firstDuplicate(int[] a) {
    for(int i=0;i<a.length;i++)
        if(a[Math.abs(a[i])-1]<0)
            return Math.abs(a[i]);
        else{
            a[Math.abs(a[i])-1]=-a[Math.abs(a[i])-1];
        }
    return -1;
}
```
