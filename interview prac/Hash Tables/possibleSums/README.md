```java
int possibleSums(int[] coins, int[] quantity) {
    HashSet<Integer> set = new HashSet<>();
    set.add(0);
    for(int i=0; i<coins.length; i++){
        ArrayList<Integer> list = new ArrayList<>();
        for(int j=0; j<=quantity[i]; j++){
            list.add(coins[i]*j);
        }
        Iterator<Integer> itr = set.iterator();
        int [] arr = set.stream().mapToInt(ele->ele).toArray();

        for(int k : arr){
            //System.out.println(k);
            for(int m=0; m<list.size(); m++) set.add(k + list.get(m));
        }
    }
    return set.size()-1;
    
}
```

##### 차이가 뭘까?? 아래꺼는 시간초과가 뜸->이유는 아래의 경우 iterator를 만들고 set을 array로 만드는 것이 계속 반복됨
```java
int possibleSums(int[] coins, int[] quantity) {
    HashSet<Integer> set = new HashSet<>();
	    set.add(0);
	    for(int i=0; i<coins.length; i++){
	        for(int j=0; j<=quantity[i]; j++){
	        	Iterator<Integer> itr = set.iterator();
	        	//System.out.println(coins[i]*j);
	        	int [] arr = set.stream().mapToInt(ele->ele).toArray();
	          
	            for(int k : arr){
	            	set.add(k + coins[i]*j);
	            }
	        }
	    }	    
	    
		//System.out.println(set.size()-1);
		return set.size()-1;    
}
```