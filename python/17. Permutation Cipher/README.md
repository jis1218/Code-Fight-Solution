For password = "iamthebest" and
key = "zabcdefghijklmnopqrstuvwxy", the output should be
permutationCipher(password, key) = "hzlsgdadrs".

```python
def permutationCipher(password, key):
    table = str.maketrans('abcdefghijklmnopqrstuvwxyz', key)
    return password.translate(table)
```