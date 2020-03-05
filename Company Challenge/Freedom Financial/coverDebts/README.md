```python
def coverDebts(s, debts, interests):
    debts = [x for _,x in sorted(zip(interests, debts), reverse=True)]
    interests = [x*0.01 for x in sorted(interests, reverse=True)]
    pay = s*0.1
    idx=0
    sum = 0    
    while(True):
        temp_pay = pay
        while(temp_pay!=0):
            diff=debts[idx]-temp_pay
            if diff>0:                
                sum += temp_pay
                debts[idx] = diff
                break
            elif diff<=0:
                sum += debts[idx]
                debts[idx]=0
                temp_pay = diff*-1
            idx += 1
            if idx == len(debts): 
                return sum                                   
        debts = [a*(b+1) for a,b in zip(debts, interests)]
```