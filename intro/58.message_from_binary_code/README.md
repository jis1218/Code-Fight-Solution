String messageFromBinaryCode(String code) {
	String result = "";
	ArrayList<String> list = new ArrayList<>();
	int i=0;
	while(true){

			list.add(code.substring(8*i, 8*i+8));
			System.out.println(list.get(i));


			if(8*i+8>=code.length()){
					break;
			}
			i++;
	}

	for(String a : list){
			result += stringToChar(a);
	}

	return result;
	}

	public String stringToChar(String a){

	    int b = Integer.parseInt(a);
	    int sum = 0;
	    int j = 0;
	    while(true){
	        sum = b%10*(int)Math.pow(2, j) + sum;
	        b /= 10;
	        j++;

	        if(b==0){
	            break;
	        }
	    }

	    char res = (char) sum;

	    return String.valueOf(res);
	}
