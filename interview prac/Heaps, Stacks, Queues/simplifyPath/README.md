Given an absolute file path (Unix-style), shorten it to the format /<dir1>/<dir2>/<dir3>/....

Here is some info on Unix file system paths:

/ is the root directory; the path should always start with it even if it isn't there in the given path;
/ is also used as a directory separator; for example, /code/fights denotes a fights subfolder in the code folder in the root directory;
this also means that // stands for "change the current directory to the current directory"
. is used to mark the current directory;
.. is used to mark the parent directory; if the current directory is root already, .. does nothing.
Example

For path = "/home/a/./x/../b//c/", the output should be
simplifyPath(path) = "/home/a/b/c".

```java
String simplifyPath(String path) {
    
    Stack<String> stack = new Stack<>();
	    
	    String spl[] = path.split("/");
	    
	    for(String s : spl){	    	
	    	System.out.println(s);
	    	if(s.equals("..") && !stack.isEmpty()){
	    		stack.pop();
	    	}else if(!s.equals("..") && !s.equals(".") && !s.equals("") ){
	    		stack.push(s);
	    	}	    		    	
	    }
    if(stack.isEmpty()) return "/";
	    StringBuilder sb = new StringBuilder();
	    while(!stack.isEmpty()){
	    	sb.insert(0, "/"+stack.pop());
	    }	    
	    return sb.toString();	
}
```