```python
def salesLeadsScore(names, time, netValue, isOnVacation):
    gop = [[t*n, name] for t, n, name, f in zip(time, netValue, names, isOnVacation) if f is False]
    print(gop)
    return [b for a, b in sorted(gop, key=functools.cmp_to_key(compare))]

def compare(x, y):
	if(x[0] < y[0]):
		return 1
	elif(x[0] > y[0]):
		return -1
	else:               
		if(x[1] < y[1]):
			return -1 
		elif(x[1] > y[1]):
			return 1
		else:
			return 0
    

```
