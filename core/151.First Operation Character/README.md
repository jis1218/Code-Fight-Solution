Given a string which represents a valid arithmetic expression, find the index of the character in the given expression corresponding to the arithmetic operation which needs to be computed first.

Note that several operations of the same type with equal priority are computed from left to right.

See the explanation of the third example for more details about the operations priority in this problem.

Example

For expr = "(2 + 2) * 2", the output should be
firstOperationCharacter(expr) = 3.

There are two operations in the expression: + and *. The result of + should be computed first, since it is enclosed in parentheses. Thus, the output is the index of the '+' sign, which is 3.

```java
int firstOperationCharacter(String expr) {    
        
    int deep = 0;
    int max_deep = 0;
    boolean IsPlus = true;
    int result_index = expr.length();
    for(int i=0; i<expr.length(); i++)
    {
        if (expr.charAt(i) == '(')
        {
            deep++;
        }else if(expr.charAt(i) == ')')
        {
            deep--;
        }else if(expr.charAt(i) == '+')
        {
            if (deep==max_deep && result_index > i && IsPlus)
            {
                result_index = i;
            }else if (deep > max_deep)
            {
                result_index = i;
                IsPlus = true;
                max_deep = Math.max(deep, max_deep);
            }                    
        }else if(expr.charAt(i) == '*')
        {
            if(deep==max_deep && IsPlus)
            {
                result_index = i;
                IsPlus = false;
            }else if(deep > max_deep)
            {
                result_index = i;
                IsPlus = false;
                max_deep = Math.max(deep, max_deep);
            }
        }

    }
    return result_index;
        
}
```