
#### KMP 알고리즘 이용
#### scanner를 쓸 때 nextLine()을 써야 enter후 입력이 된다.
#### 만약 next()를 쓴다면 스페이스바만 눌러도 입력이 되기 때문이다.
#### 밑에 while 대신 if를 써도 되긴 한다.


```java

import java.util.ArrayList;
import java.util.Scanner;

class Main{
    	public static void main(String[] args) {
		
        Scanner scanner = new Scanner(System.in);
            
		String a = scanner.nextLine();
		String b = scanner.nextLine();
        
        int [] result = KMPAlgo(a,b);
        System.out.println(result.length);
        for(int i : result) System.out.println(i);

	}
	
	public static int[] findTable(String b){
		int[] arrB = new int[b.length()];
		int j=0;
		for(int i=1; i< arrB.length; i++){
			while(j>0 && b.charAt(i)!=b.charAt(j)){
				j = arrB[j-1];
			}
			if(b.charAt(i)==b.charAt(j)){
				arrB[i] = ++j;
			}
		}
		
		return arrB;
	}
	
	public static int[] KMPAlgo(String a, String b){
		
		ArrayList<Integer> list = new ArrayList<>();
		
		int[] table = findTable(b);
		int j=0;
		for(int i=0; i<a.length(); i++){
			while(j>0 && a.charAt(i)!=b.charAt(j)){
				j = table[j-1];
			}
			if(a.charAt(i)==b.charAt(j)){
				if(j==b.length()-1){
					list.add(i-b.length()+1);
					j = table[j];
				}else{
					j++;
				}
			}
		}
		
		return list.stream().mapToInt(i->i+1).toArray();
		
	}
}
```



