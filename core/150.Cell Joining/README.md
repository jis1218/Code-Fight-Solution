```java
String[] cellsJoining(String[] table, int[][] coords) {
    int minrow = Math.min(coords[0][0], coords[1][0]);
    int maxrow = Math.max(coords[0][0], coords[1][0]);
    int mincol = Math.min(coords[0][1], coords[1][1]);
    int maxcol = Math.max(coords[0][1], coords[1][1]);
    int rowcount = -1;
    int columncount = -1;

    int firstrow = 0;
    int secondrow = 0;

    int firstcolumn = 0;
    int secondcolumn = 0;

    ArrayList<Integer> rowMid = new ArrayList<>();
    ArrayList<Integer> colMid = new ArrayList<>();
    boolean flag = true;
    for(int i=0; i<table.length; i++){
        if(table[i].charAt(0)=='+'){
            rowcount++;
            if(flag){
                flag = false;
                for(int j=0; j<table[i].length(); j++){
                    if(table[i].charAt(j)=='+'){
                        columncount++;
                        if(columncount==mincol){
                            firstcolumn = j;
                        }else if(columncount==maxcol+1){
                            secondcolumn = j;
                            break;
                        }else if(columncount>mincol && columncount<=maxcol){
                            colMid.add(j);
                        }
                    }
                }
            }else if(!flag && rowcount>minrow && rowcount<=maxrow){
                StringBuilder builder = new StringBuilder(table[i]);
                String s = "";
                for(int j=0; j<secondcolumn-firstcolumn-1; j++){
                    s+= " ";
                }
                builder.replace(firstcolumn+1, secondcolumn, s);
                if(firstcolumn==0) builder.replace(0, 1, "|");
                if(secondcolumn==table[i].length()-1) builder.replace(table[i].length()-1, table[i].length(), "|");
                table[i] = builder.toString();
            }
            if((rowcount==maxrow+1 && i==table.length-1) || (rowcount==minrow && i==0)){
					StringBuilder builder = new StringBuilder(table[i]);
					for(int j=0; j<colMid.size(); j++){
						builder.replace(colMid.get(j), colMid.get(j)+1, "-");
						table[i] = builder.toString();
					}
				}


        }else if(rowcount>=minrow && rowcount<=maxrow){
            StringBuilder builder = new StringBuilder(table[i]);
            for(int j=0; j<colMid.size(); j++){
                builder.replace(colMid.get(j), colMid.get(j)+1, " ");
                table[i] = builder.toString();
            }
        }
    }

    return table;
}
```