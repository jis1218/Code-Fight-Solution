import java.util.*;
class Solution {
    public int[][] solution(int[][] nodeinfo) {
        int[][] answer = new int[2][nodeinfo[0].length];
        Integer index[] = new Integer[nodeinfo.length];     
        Node[] nodeList = new Node[nodeinfo.length];
        ArrayList<Node> nodeArr = new ArrayList<>();
        for(int i=1; i<=nodeinfo.length; i++){
            index[i-1] = i;            
        }        
        Arrays.sort(index, new Comparator<Integer>(){
            public int compare(Integer i, Integer j){
                if(nodeinfo[i-1][1]<nodeinfo[j-1][1]){
                    return 1;
                }else if(nodeinfo[i-1][1]==nodeinfo[j-1][1]){
                    if(nodeinfo[i-1][0]>nodeinfo[j-1][0]) return 1;
                    else return -1;
                }else return -1;
            }
        });
        for(int i=0; i<nodeinfo.length; i++){
            // nodeList[i] = new Node(index[i]);
            // nodeList[i].x = nodeinfo[index[i]-1][0];
            // nodeList[i].y = nodeinfo[index[i]-1][1];
            nodeArr.add(new Node(index[i]));
            nodeArr.get(i).x = nodeinfo[index[i]-1][0];
            nodeArr.get(i).y = nodeinfo[index[i]-1][1];
        }        
        
        helper(nodeArr);
        
        // for(int i=0; i<nodeList.length; i++){            
        //     int x=0;
        //     int y=0;
        //     if(nodeList[i].leftNode!=null) x = nodeList[i].leftNode.value;
        //     if(nodeList[i].rightNode!=null) y = nodeList[i].rightNode.value;
        //     //System.out.println(nodeList[i].value + ", left = " + x + ", right = " + y);
        // }            

        ArrayList<Integer> list1 = new ArrayList<>();
        ArrayList<Integer> list2 = new ArrayList<>();
        preorder(nodeArr.get(0), list1);
        //System.out.println("");
        postorder(nodeArr.get(0), list2); 
        //System.out.println(list1.size());
        //System.out.println(list2.size());
        
        ArrayList<int[]> resultList = new ArrayList<>();
        resultList.add(list1.stream().mapToInt(Integer::intValue).toArray());
        resultList.add(list2.stream().mapToInt(Integer::intValue).toArray());
        return resultList.toArray(new int[0][0]);
    }
    
    void helper(ArrayList<Node> nodeList){
        ArrayList<Node> left = new ArrayList<>();
        ArrayList<Node> right = new ArrayList<>();
        for(int i=1; i<nodeList.size(); i++){
            if(nodeList.get(0).x>nodeList.get(i).x){
                left.add(nodeList.get(i));
            }
            if(nodeList.get(0).x<nodeList.get(i).x){
                right.add(nodeList.get(i));
            }
        }
        if(left.size()>0){
            nodeList.get(0).leftNode = left.get(0);
            helper(left);
        }
        if(right.size()>0){
            nodeList.get(0).rightNode = right.get(0);
            helper(right);
        }
        return;
    }
    
    void preorder(Node node, ArrayList<Integer> list){        
        System.out.print(node.value + ", ");
        list.add(node.value);
        if(node.leftNode!=null) preorder(node.leftNode, list);
        if(node.rightNode!=null) preorder(node.rightNode, list);
        else return;
    }
    
    void postorder(Node node, ArrayList<Integer> list){
        if(node.leftNode!=null) postorder(node.leftNode, list);
        if(node.rightNode!=null) postorder(node.rightNode, list);
        System.out.print(node.value + ", "); 
        list.add(node.value);
        return;
        
    }
}

class Node{
    Node leftNode;
    Node rightNode;
    Node parentNode;
    
    int value;
    int x;
    int y;
    Node(int value){
        this.value = value;
    }
}