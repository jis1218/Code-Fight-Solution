```java
ArrayList<int []> result = new ArrayList<>();

int[][] nQueens(int n) {
    
    boolean[] visit = new boolean[n];
    Arrays.fill(visit, false);
    ArrayList<Integer> intList = new ArrayList<>();
    helper(n, intList, visit, -1);
    return result.toArray(new int[0][0]);
}

void helper(int n, ArrayList<Integer> intList, boolean[] visit, int lastNum){		
    if(intList.size()==n){
			result.add(intList.stream().mapToInt(i -> i).toArray());
			return;
    }
    for(int i=1; i<=n; i++){
        if(!visit[i-1] && i!=lastNum-1 && i!=lastNum+1){
            boolean flag = true;
            for(int j=1; j<=intList.size(); j++){
                if(Math.abs(i-intList.get(j-1))==Math.abs(intList.size()+1-j)){
                    flag = false;
                };
            }
            if(flag){
                intList.add(i);
                visit[i-1] = true;
                helper(n, intList, visit, i);
                intList.remove(intList.size()-1);
                visit[i-1] = false;
            }				
        }			
    }
    
}

```