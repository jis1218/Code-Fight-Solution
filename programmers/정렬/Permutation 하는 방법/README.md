```java
import java.util.HashSet;
import java.util.Iterator;
class Solution {
    public int solution(String numbers) {
        for(int i=1; i<=numbers.length(); i++){
            perm(numbers, "", i);
        }
        
		Iterator<Integer> itr = set.iterator();
		int count = 0;
		while(itr.hasNext()){
			int s = itr.next();
			if(isPrime(s)){
				count++;
			}
		}
		return count;
    }
    
    public boolean isPrime(int n){
        if(n==2) return true;
        if(n==1 || n%2==0) return false;
		for(int i=3; i<=(int)Math.sqrt(n); i+=2){
			if(n%i==0) return false;
		}
		return true;
    }
    
    HashSet<Integer> set = new HashSet<>();
    
    public void perm(String number, String result, int num){
        	if(result.length()==num){			
			    set.add(Integer.valueOf(result));
			    return;
		    }
		for(int i=0; i<number.length(); i++){
			char c = number.charAt(i);
			result += c;
			perm(number.substring(0, i) + number.substring(i+1, number.length()), result, num);
			result = result.substring(0, result.length()-1);
		}
    }
}
```