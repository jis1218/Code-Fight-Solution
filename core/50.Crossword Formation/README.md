int crosswordFormation(String[] words) {
    int a1, a2, a3, a4, a5, a6, a7, a8;
    int[][] order = {
        {1, 2, 3}, {1, 3, 2}, {2, 1, 3}, {2, 3, 1}, {3, 1, 2}, {3, 2, 1}
    };
    
    int result = 0;
    String a=words[0];
    String b;
    String c;
    String d;
    for(int aa=0; aa<6; aa++){
        
        b=words[order[aa][0]];
        c=words[order[aa][1]];
        d=words[order[aa][2]];
        for(int i=0; i<a.length()-2; i++){
            for(int j=0; j<b.length()-2; j++){
                if(a.charAt(i)==b.charAt(j)){
                    a1 = i;
                    a2 = j;                
                    for(int k=a2+2; k<b.length(); k++){
                        for(int l=0; l<c.length()-2; l++){
                            if(b.charAt(k)==c.charAt(l)){
                                a3 = k;
                                a4 = l;
                                for(int m=a4+2; m<c.length(); m++){
                                    for(int n=d.length()-1; n>=2; n--){
                                        if(c.charAt(m)==d.charAt(n)){
                                            a5 = m;
                                            a6 = n;
                                            for(int p=a6-2; p>=0; p--){
                                                for(int q=a1+2; q<a.length(); q++){
                                                    a7 = p;
                                                    a8 = q;
                                                    if(d.charAt(p)==a.charAt(q)){
                                                        if(a3-a2==a6-a7 && a8-a1==a5-a4){
                                                            result++;
                                                            System.out.println(b + c + d);
                                                            System.out.println(a1 + ", " + a2 + ", " + a3 + ", " + a4 + ", "
                                                                              + a5 + ", " + a6 + ", " + a7 + ", " +a8);
                                                        }
                                                    }
                                                }
                                            }
                                        }
                                    }
                                }
                            }
                        }
                    }
                }
            }
        }
        
        
    }
        
    
    return result*2;
}