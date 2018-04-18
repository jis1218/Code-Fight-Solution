
For s = "We expect the %f%% growth this week", the output should be
newStyleFormatting(s) = "We expect the {}% growth this week".


```python
def newStyleFormatting(s):

    i=1
    while i<len(s):        
        if s[i-1]=="%" and s[i]=="%":
            s = s[:i-1] + s[i:] #s[:i]이면 i번째 전까지, s[i+1:]이면 i+1번째 포함하여...

        elif s[i-1]=="%" and s[i] in ['s', 'c', 'd', 'f', 'x', 'o', 'h', 'e', 'g', 'a', 't']:
            s = s[:i-1] + "{}" + s[i+1:]
        
        i = i+1
        
    return s
```

```python
import re
def newStyleFormatting(s):
    return "%".join([re.sub("%([bcdeEfFgGnosxX])","{}",S) for S in s.split("%%")])
```