```java
import java.util.*;
import java.util.stream.*;

class Solution {
    public int[] solution(String[] info, String[] query) {
        int[] answer = {};
        Tree root = new Tree("root", new HashMap<>(), new ArrayList<>());
        
        for(int i = 0; i<info.length; i++) {
            String[] inform = info[i].split(" ");    
            
            int score = Integer.valueOf(inform[4]);
            
            addTreeChain(inform, 0, root, score);
        }
        
        ArrayList<Integer> result = new ArrayList<>();
        
        for(String singleQuery : query) {
            result.add(analyzeQuery(root, singleQuery));
        }
        
        return result.stream().mapToInt(i->i).toArray();
    }
    
    public void addTreeChain(String[] inform, int index, Tree tree, int score) {
        Tree childTree = tree.getMatchTree(inform[index]);
        Tree masterChildTree = tree.getMatchTree("-");
        
        if(index == 3) {
            childTree.addPeople(score);
            masterChildTree.addPeople(score);            
            return;
        }
        
        addTreeChain(inform, index + 1, childTree, score);
        addTreeChain(inform, index + 1, masterChildTree, score);
        
    }
    
    public int analyzeQuery(Tree root, String singleQuery) {
        String parsed[] = parseQuery(singleQuery);
        
        ArrayList<Integer> people = 
            root.getMatchTree(parsed[0])
            .getMatchTree(parsed[1])
            .getMatchTree(parsed[2])
            .getMatchTree(parsed[3])
            .getPeople();        
        
        Integer score = Integer.valueOf(parsed[4]);
        
        int count = (int)people.stream().filter(no -> no>=score).count();
        
        return count;
    }
    
    public String[] parseQuery(String singleQuery) {
        String[] temp = singleQuery.split(" and ");
        String parsedQuery[] = new String[5];
        String tempPart[] = temp[3].split(" ");
        parsedQuery[0] = temp[0];
        parsedQuery[1] = temp[1];
        parsedQuery[2] = temp[2];
        parsedQuery[3] = tempPart[0];
        parsedQuery[4] = tempPart[1];
        
        return parsedQuery;
    }
    
    public class Tree {
        String character;
        Map<String, Tree> trees = new HashMap<>();
        ArrayList<Integer> people = new ArrayList<>();
        
        public Tree(String character) {
            this.character = character;
        }
        
        public Tree(String character, Map<String, Tree> trees, ArrayList<Integer> people) {
            this.character = character;
            this.trees = trees;
            this.people = people;
        }
        
        public void addTree(Tree tree) {
            this.trees.put(character, tree);
        }
        
        public void addPeople(int no) {
            this.people.add(no);
            
        }
        
        public ArrayList<Integer> getPeople() {
            return this.people;
        }
        
        public int peopleSize() {
            return this.people.size();
        }
        
        public Tree getMatchTree(String character) {
            
            if(trees.containsKey(character)) {
                return trees.get(character);
            }
            
            Tree childTree = new Tree(character);
            trees.put(character, childTree);
            
            return childTree;            
        }
    }
}
```
##### cache 사용 버전(더 늦은것 같다)
```java
import java.util.*;
import java.util.stream.*;

class Solution {
    private Map<String, ArrayList<Integer>> cache = new HashMap<>();
    
    public int[] solution(String[] info, String[] query) {
        int[] answer = {};
        Tree root = new Tree("root", new HashMap<>(), new ArrayList<>());
        
        
        for(int i = 0; i<info.length; i++) {
            String[] inform = info[i].split(" ");    
            
            int score = Integer.valueOf(inform[4]);
            
            addTreeChain(inform, 0, root, score, "");
        }
        
        ArrayList<Integer> result = new ArrayList<>();
        
        for(String singleQuery : query) {
            result.add(analyzeQuery(root, singleQuery));
        }
        
        return result.stream().mapToInt(i->i).toArray();
    }
    
    public void addTreeChain(String[] inform, int index, Tree tree, int score, String cacheString) {
        Tree childTree = tree.getMatchTree(inform[index]);
        Tree masterChildTree = tree.getMatchTree("-");
        
        if(index == 3) {
            childTree.addPeople(score);
            masterChildTree.addPeople(score);   
            cache.put(cacheString + inform[index], childTree.people);
            cache.put(cacheString + "-", masterChildTree.people);
            return;
        }
        
        addTreeChain(inform, index + 1, childTree, score, cacheString + inform[index]);
        addTreeChain(inform, index + 1, masterChildTree, score, cacheString + "-");
        
    }
    
    public int analyzeQuery(Tree root, String singleQuery) {
        String parsed[] = parseQuery(singleQuery);
        String key = parsed[0].concat(parsed[1]).concat(parsed[2]).concat(parsed[3]);
        ArrayList<Integer> people = cache.get(key);
        if(people==null) return 0;
        
        Integer score = Integer.parseInt(parsed[4]);
        // ArrayList<Integer> people = 
        //     root.getMatchTree(parsed[0])
        //     .getMatchTree(parsed[1])
        //     .getMatchTree(parsed[2])
        //     .getMatchTree(parsed[3])
        //     .getPeople();        
        int count = 0;
        for(int no : people) {
            if(no>=score) {
                count++;
            }
        }
        
        return count;
    }
    
    public String[] parseQuery(String singleQuery) {
        String[] temp = singleQuery.split(" and ");
        String parsedQuery[] = new String[5];
        String tempPart[] = temp[3].split(" ");
        parsedQuery[0] = temp[0];
        parsedQuery[1] = temp[1];
        parsedQuery[2] = temp[2];
        parsedQuery[3] = tempPart[0];
        parsedQuery[4] = tempPart[1];
        
        return parsedQuery;
    }
    
    public class Tree {
        String character;
        Map<String, Tree> trees = new HashMap<>();
        ArrayList<Integer> people = new ArrayList<>();
        
        public Tree(String character) {
            this.character = character;
        }
        
        public Tree(String character, Map<String, Tree> trees, ArrayList<Integer> people) {
            this.character = character;
            this.trees = trees;
            this.people = people;
        }
        
        public void addTree(Tree tree) {
            this.trees.put(character, tree);
        }
        
        public void addPeople(int no) {
            this.people.add(no);
            
        }
        
        public ArrayList<Integer> getPeople() {
            return this.people;
        }
        
        public int peopleSize() {
            return this.people.size();
        }
        
        public Tree getMatchTree(String character) {
            
            if(trees.containsKey(character)) {
                return trees.get(character);
            }
            
            Tree childTree = new Tree(character);
            trees.put(character, childTree);
            
            return childTree;            
        }
    }
}
```