---
jupyter:
  jupytext:
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.2'
      jupytext_version: 1.5.0
  kernelspec:
    display_name: Python 3
    language: python
    name: python3
---

### <font color="blue"> Import Library </font>

```python
import pandas as pd
from apyori import apriori
import time
```

### <font color='blue'> Apriori function </font>

```python
def apriori_function(dataset,min_support):
    start = time.process_time()
    association_rules = apriori(dataset, min_support=min_support/100)
    elapsed_time_secs = time.time() - start
    return elapsed_time_secs
```

### <font color='blue'> Apriori for T10I4D100K </font>

```python
T10I4D100K = [i.strip().split() for i in open("T10I4D100K.dat").readlines()]
```

```python
T10I4D100K_relative_support=[0.3,0.5,1,1.5,2,2.5,3]
```

```python
T10I4D100K_apriori_time=[apriori_function(T10I4D100K, i) for i in T10I4D100K_relative_support]
```

```python
T10I4D100K_apriori_time
```

```python
T10I4D100K_apriori=pd.DataFrame()
T10I4D100K_apriori["relative_support"]=T10I4D100K_relative_support
T10I4D100K_apriori['model_running_time']=T10I4D100K_apriori_time
```

```python
T10I4D100K_apriori.to_csv("T10I4D100K_apriori.csv",index=False)
```

### <font color='blue'> Ariori for T40I10D100K </font>

```python
T40I10D100K=[i.strip().split() for i in open("T40I10D100K.dat").readlines()]
```

```python
T40I10D100K_relative_support=[0.3,0.5,1,1.5,2,2.5,3]
```

```python
T40I10D100K_apriori_time=[apriori_function(T40I10D100K, i) for i in T40I10D100K_relative_support]
```

```python
T40I10D100K_apriori=pd.DataFrame()
T40I10D100K_apriori["relative_support"]=T40I10D100K_relative_support
T40I10D100K_apriori['model_running_time']=T10I4D100K_apriori_time
```

```python
T40I10D100K_apriori.to_csv("T40I10D100K_apriori.csv",index=False)
```

### <font color='blue'> Apriori for  mushroom </font>

```python
mushroom=[i.strip().split() for i in open("mushroom.dat").readlines()]
```

```python
mushroom_relative_support=[4,7,10,13,16,20]
```

```python
mushroom_apriori_time=[apriori_function(mushroom, i) for i in mushroom_relative_support]
```

```python
mushroom_apriori=pd.DataFrame()
mushroom_apriori["relative_support"]=mushroom_relative_support
mushroom_apriori['model_running_time']=mushroom_apriori_time
```

```python
mushroom_apriori.to_csv("mushroom_apriori.csv",index=False)
```
