Given an encoded string, return its corresponding decoded string.

The encoding rule is: k[encoded_string], where the encoded_string inside the square brackets is repeated exactly k times. Note: k is guaranteed to be a positive integer.

Note that your solution should have linear complexity because this is what you will be asked during an interview.

Example

For s = "4[ab]", the output should be
decodeString(s) = "abababab";

For s = "2[b3[a]]", the output should be
decodeString(s) = "baaabaaa";

For s = "z1[y]zzz2[abc]", the output should be
decodeString(s) = "zyzzzabcabc".

```java
String decodeString(String s) {
    Deque<String> queue = new ArrayDeque<>();
		String temp_num = "";
		String temp_str = "";
		for(int i=0; i<s.length(); i++){
			char ch = s.charAt(i);
			if(ch>='0' && ch<='9'){
				if(!temp_str.equals("")){
					queue.push(temp_str);
					temp_str = "";
				}
				temp_num += ch;
				
			}else if(ch>='a' && ch<='z'){
				if(!temp_num.equals("")){
					queue.push(temp_num);
					temp_num = "";
				}
				temp_str += ch;
			}else if(ch==']'){
				queue.push(temp_str);
				String temp = "";
				String result = "";
				while(!isInteger(queue.peek())){
					temp = queue.poll() + temp;
				}
				if(isInteger(queue.peek())){
					int k = Integer.parseInt(queue.poll());
					System.out.println(k + ", " + temp);
					for(int j=0; j<k; j++){
						result += temp;
					}
				}
				System.out.println(result);
				if(!temp.equals("")){
					queue.push(result);
				}
				temp_str = "";
			}else if(ch == '['){
				if(!temp_num.equals("")){
					queue.push(temp_num);
					temp_num = "";
				}
				if(!temp_str.equals("")){
					queue.push(temp_str);
					temp_str = "";
				}
			}			
		}
    if(!temp_str.equals("")) {			
			queue.push(temp_str);
		}
		String result = "";
		while(!queue.isEmpty()){
			result = queue.pop() + result;
						
		}
		
		return result;

}

boolean isInteger(String s){
    try{
        Integer.valueOf(s);
    }catch(Exception e){
        return false;
    }
    return true;
}

```

```python
def decodeString(s):
    li = []
    for i in s:
        if i==']':
            temp = ''
            while li[-1]!='[':
                temp = li.pop() + temp
            li.pop()
            digit = ''
            while len(li)!=0 and li[-1].isdigit():
                digit = li.pop() + digit
            li.append(int(digit)*temp)
        else:
            li.append(i)
    return ''.join(li)
```