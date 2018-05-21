You decided to found your own startup company and now want to choose a proper name for it. There are three large companies that you want to compete against, and since their names are quite popular you want to use their names as a starting point. You want to use only popular characters in the name of your company, but not too mainstream. You consider a character to be popular if it appears in at least two company names, and consider it to be mainstream if it appears in all three.
Given the names of the companies, return the list of characters that are popular but not mainstream sorted by their ASCII codes.

##### 집합을 잘 알고 있으면 됨
```python
def startupName(companies):
    comp1 = set(companies[0])
    comp2 = set(companies[1])
    comp3 = set(companies[2])
    res = ((comp1^comp2)&comp3) | ((comp1^comp3)&comp2) | ((comp2^comp3)&comp1) #여기를 풀었음
    return sorted(list(res))
```