##### 처음에 Map으로만 풀었다가 시간 fail이 나서 tree를 미리 만들어주는 것으로 바꿨는데도 안됐다.
##### for문에서 break되는 조건을 잘 찾는 것이 중요!!

```java
import java.util.*;

class Solution {
    public int[] solution(String[] enroll, String[] referral, String[] seller, int[] amount) {       
        Map<String, Integer> profits = new HashMap<>();        
        Map<String, String> parents = new HashMap<>();
        Map<String, ArrayList<String>> tree = new HashMap<>();
        
        for(int i=0; i<enroll.length; i++) {
            parents.put(enroll[i], referral[i]);
            profits.put(enroll[i], 0);
            ArrayList<String> list = new ArrayList<>();
            list.add(enroll[i]);
            tree.put(enroll[i], list);
        }
        
        for(String person : enroll) {
            makeTree(tree, parents, person);
        }
        
        List<Integer> answerList = new ArrayList<>();
        
        for(int i=0; i<seller.length; i++) {            
            profitDivider(profits, tree, seller[i], amount[i] * 100);
        }
        
        for(String person : enroll) {
            answerList.add(profits.get(person));
        }
        
        return answerList.stream().mapToInt(i->i).toArray();
    }
    
    private void makeTree(Map<String, ArrayList<String>> tree, Map<String, String> parents, String person) {
        String parent = parents.get(person);   
        if(parent.equals("-")) return;
        if(tree.get(person).size()>1) return;   
        
        makeTree(tree, parents, parent);   
        tree.get(person).addAll(tree.get(parent));
    }
    
    private void profitDivider(Map<String, Integer> profits, Map<String, ArrayList<String>> tree, String seller, Integer amount) {
        
        ArrayList<String> parentList = tree.get(seller);        
        
        for(String parent : parentList) {
            int otherBenefit = (int)(amount * 0.1);
            if(amount - otherBenefit == 0) break;
            profits.put(parent, profits.get(parent) + amount - otherBenefit);
            amount = otherBenefit;
        }
    }
}
```

```java
import java.util.*;

class Solution {
    public int[] solution(String[] enroll, String[] referral, String[] seller, int[] amount) {       
        Map<String, Integer> profits = new HashMap<>();        
        Map<String, String> parents = new HashMap<>();
        
        for(int i=0; i<enroll.length; i++) {
            parents.put(enroll[i], referral[i]);
            profits.put(enroll[i], 0);
        }
        
        List<Integer> answerList = new ArrayList<>();
        
        for(int i=0; i<seller.length; i++) {            
            profitDivider(profits, parents, seller[i], amount[i] * 100);
        }
        
        for(String person : enroll) {
            answerList.add(profits.get(person));
        }
        
        return answerList.stream().mapToInt(i->i).toArray();
    }    
   
    private void profitDivider(Map<String, Integer> profits, Map<String, String> parent, String seller, int amount) {
        if(seller.equals("-") || amount == 0) return;        
        int otherBenefit = (int)(amount * 0.1);       
        profits.put(seller, profits.get(seller) + amount - otherBenefit);
        
        profitDivider(profits, parent, parent.get(seller), otherBenefit);
        
    }
}
```