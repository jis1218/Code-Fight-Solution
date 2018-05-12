A cryptarithm is a mathematical puzzle for which the goal is to find the correspondence between letters and digits, such that the given arithmetic equation consisting of letters holds true when the letters are converted to digits.
You have an array of strings crypt, the cryptarithm, and an an array containing the mapping of letters and digits, solution. The array crypt will contain three non-empty strings that follow the structure: [word1, word2, word3], which should be interpreted as the word1 + word2 = word3 cryptarithm.
If crypt, when it is decoded by replacing all of the letters in the cryptarithm with digits using the mapping in solution, becomes a valid arithmetic equation containing no numbers with leading zeroes, the answer is true. If it does not become a valid arithmetic solution, the answer is false.
```java
boolean isCryptSolution(String[] crypt, char[][] solution) {
    double[] res = new double[3];
    
    for(int m=0; m<crypt.length; m++){
        String temp = crypt[m];
        for(int i=0; i<crypt[m].length(); i++){            
            for(int j=0; j<solution.length; j++){
                if(temp.charAt(i)==solution[j][0]){
                    temp = temp.replace(temp.charAt(i), solution[j][1]);
                    if(i==0){
                        if(temp.charAt(i)=='0' && temp.length()>1) return false;
                    }
                    break;
                }
            }
        }
        res[m] = Double.valueOf(temp);
    }
    
    if(res[0]+res[1]==res[2]) return true;
    else return false; 
}
```