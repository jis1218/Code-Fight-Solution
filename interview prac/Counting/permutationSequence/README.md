The set [1, 2, 3, ... , n] contains a total of n! unique permutations. List all the permutations for an integer n in lexicographical order and return the kth permutation in the sequence as a string. To build this string, concatenate decimal representations of permutation elements from left to right without any delimiters.

Example

For n = 3 and k = 3, the output should be
permutationSequence(n, k) = "213".

The ordered list of possible permutations for 3! is:

  1) "123"
  2) "132"
  3) "213"
  4) "231"
  5) "312"
  6) "321"
The 3rd permutation in the lexicographically ordered sequence is "213".

```python
def permutationSequence(n, k):
    k -= 1
    li = [i for i in range(1, n+1)]
    #print(li)
    perm = 1
    cnt = 1
    while(perm<=k):
        cnt += 1
        perm *= cnt
    
    #print('cnt = ', cnt)
    perm //= cnt
    #print('perm = ', perm)
    #print('n-cnt = ', n-cnt)
    store = [0]*(n-cnt)
    while True:
        store.append(k//perm)
        k = k%perm 
        cnt-=1    
        if cnt==0:
            break 
        perm //= cnt
    result = ''
    for i in store:
        result += str(li[i])
        del li[i]
    return result
```