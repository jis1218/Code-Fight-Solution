
##### 이 문제에서 가장 시간이 많이 걸린건 ArrayList<int[]> 를 int[][]로 바꾸는것... 처음부터 어렵게 생각했나보다. 

##### ArrayList<int[]> -> int[][]
```java
list.toArray(new int[0][0]);
```

##### ArrayList<Integer> -> int[]
```java
list.add(spring.stream().mapToInt(Integer::intValue).toArray());
```

##### 나의 답 - 리스트를 전역변수로 설정하였다. 그리고 경우의 수를 리스트에 넣은다음 배열로 변환해줬다.
```java
ArrayList<int[]> list = new ArrayList<>();

int[][] climbingStaircase(int n, int k) {
    ArrayList<Integer> spring = new ArrayList<>();
    helper(n, k, spring);
    
    return list.toArray(new int[0][0]);
}

void helper(int n, int k, ArrayList<Integer> spring){
    if(n==0){
        list.add(spring.stream().mapToInt(Integer::intValue).toArray());
    }
    for(int i=1; i<=Math.min(n, k); i++){
        spring.add(i);
        helper(n-i, k, spring);
        spring.remove(spring.size()-1);
    }    
}
```

##### 나랑 가장 비슷하게 푼사람
```java
int[][] climbingStaircase(int n, int k) {
        solution = new int[n];
        climb(n,k,0);
        
        return results.toArray(new int[results.size()][]);
}

int[] solution;
List<int[]> results = new ArrayList<int[]>();

void climb(int remainingSteps, int jump, int solutionSize) {
        
    if(remainingSteps==0) {
            results.add(Arrays.copyOf(solution,solutionSize));
             return;
     }
     
     int maxJump = Math.min(remainingSteps,jump);
     for(int i=1;i<=maxJump;i++) {
             solution[solutionSize] = i;
             climb(remainingSteps-i, jump, solutionSize+1);
             solution[solutionSize] = 0;
     }  
}
```

##### 이렇게도 하였다.
```java
int n, k;
List<List<Integer>> r = new ArrayList<>();

int[][] climbingStaircase(int n, int k) {
    this.n = n;
    this.k = k;
    f(new ArrayList<>(), 0);
    return r.stream().map(l -> l.stream().mapToInt(i -> i).toArray()).toArray(int[][]::new);
}

void f(List<Integer> l, int sum) {
    if (sum > n) return;        
    if (sum == n) {
        r.add(l);
    } else {
        for (int i = 1; i <= k; ++i) {
            List<Integer> x = new ArrayList<>(l);
            x.add(i);
            f(x, sum + i);
        }
    }
}
```

#####
```java
int[][] climbingStaircase(int n, int k) {
   List<List<Integer>> result = new ArrayList<>();
   backtrack(n, k, result, new ArrayList<Integer>());
   int[][] re = new int[result.size()][0];
   for (int i = 0; i < result.size(); i++) {
      re[i] = new int[result.get(i).size()];
      for (int j = 0; j < result.get(i).size(); j++) {
         re[i][j] = result.get(i).get(j);
      }
   }
   return re;
}

void backtrack(int n, int k, List<List<Integer>> result, List<Integer> tempList) {
   if (n == 0) result.add(new ArrayList<>(tempList));
   for (int i = 1; i <= k; i++) {
      if (n >= i) {
         tempList.add(i);
         backtrack(n-i, k, result, tempList);
         tempList.remove(tempList.size()-1);
      }
   }
   
}
```