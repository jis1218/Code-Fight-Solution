Given a word, check whether it is a palindrome or not. A string is considered to be a palindrome if it reads the same in both directions.
Example
For word = "aibohphobia", the output should be
isWordPalindrome(word) = true;
For word = "hehehehehe", the output should be
isWordPalindrome(word) = false.
```python
def isWordPalindrome(word):
    return word == word[::-1]
```

##### arr[A:B:C]의 의미는, index A 부터 index B 까지 C의 간격으로 배열을 만들어라는 말입니다. 만약 A가 None 이라면, 처음부터 라는 뜻이고 B가 None 이라면, 할 수 있는 데까지 (C가 양수라면 마지막 index까지, C가 음수라면 첫 index까지가 되겠습니다.)라는 뜻입니다. 마지막으로 C가 None 이라면 한 칸 간격으로 라는 뜻입니다. 

```python

arr = range(10) #arr [0,1,2,3,4,5,6,7,8,9] 
arr[::2] # 처음부터 끝까지 두 칸 간격으로 [0,2,4,6,8] 
arr[1::2] # index 1 부터 끝까지 두 칸 간격으로 [1,3,5,7,9] >> 
arr[::-1] # 처음부터 끝까지 -1칸 간격으로 ( == 역순으로) [9,8,7,6,5,4,3,2,1,0] 
arr[::-2] # 처음부터 끝까지 -2칸 간격으로 ( == 역순, 두 칸 간격으로) [9,7,5,3,1] 
arr[3::-1] # index 3 부터 끝까지 -1칸 간격으로 ( == 역순으로) [3,2,1,0] >> 
arr[1:6:2] # index 1 부터 index 6 까지 두 칸 간격으로 [1,3,5]
```

##### 출처: http://kascia.tistory.com/3 [Kascia's blog]
