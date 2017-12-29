You are taking part in an Escape Room challenge designed specifically for programmers. In your efforts to find a clue, you've found a binary code written on the wall behind a vase, and realized that it must be an encrypted message. After some thought, your first guess is that each consecutive 8 bits of the code stand for the character with the corresponding extended ASCII code.
Assuming that your hunch is correct, decode the message.
Example
For code = "010010000110010101101100011011000110111100100001", the output should be
messageFromBinaryCode(code) = "Hello!".
The first 8 characters of the code are 01001000, which is 72 in the binary numeral system. 72 stands for H in the ASCII-table, so the first letter is H.
Other letters can be obtained in the same manner.

```java
String messageFromBinaryCode(String code) {
	String result = "";
	ArrayList<String> list = new ArrayList<>();
	int i=0;
	while(true){
			/**
			* String 값을 8개 단위로 나눠서 arraylist에 넣어준다.
			**/
			list.add(code.substring(8*i, 8*i+8));

			/**
			* 만약 범위를 넘어가게 되면 while 문을 빠져나온다.
			**/
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

	/**
	* 자른 string을 Integer로 바꿔준 후 2진수 -> 10진수로 바꿔준다.
	**/
	public String stringToChar(String a){

	    int b = Integer.parseInt(a);
	    int sum = 0;
	    int j = 0;
	    while(true){
	        sum = b%10*(int)Math.pow(2, j) + sum; //2진수를 10진수로 바꿔주는 로직
	        b /= 10;
	        j++;

	        if(b==0){
	            break;
	        }
	    }

	    char res = (char) sum;

	    return String.valueOf(res);
	}
	```
