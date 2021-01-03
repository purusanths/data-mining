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

### <font color="blue" >Import Library </font>

```python
import pandas as pd
from pyECLAT import ECLAT
import time
```

### <font color='blue'> Eclat function </font>

```python
def eclat_function(dataset,min_support):
    eclat_instance = ECLAT(data=dataset, verbose=False)
    start = time.process_time()
    get_ECLAT_indexes, get_ECLAT_supports = eclat_instance.fit(min_support=min_support,verbose=False,min_combination=1,
                                                           max_combination=2)
    elapsed_time_secs = time.time() - start
    return elapsed_time_secs
```

### <font color='blue'> Eclat for T10I4D100K </font>

```python
T10I4D100K = [i.strip().split() for i in open("T10I4D100K.dat").readlines()]
```

```python
T10I4D100K=pd.DataFrame(T10I4D100K)
for i in range(len(T10I4D100K.columns)):
    T10I4D100K[i]=T10I4D100K[i].astype(str)+"_item"
    T10I4D100K[i].replace("None_item","None",inplace=True)
```

```python
T10I4D100K_relative_support=[0.3,0.5,1,1.5,2,2.5,3]
```

```python
T10I4D100K_eclat_time=[eclat_function(T10I4D100K, i) for i in T10I4D100K_relative_support]
```

```python
T10I4D100K_eclat=pd.DataFrame()
T10I4D100K_eclat["relative_support"]=T10I4D100K_relative_support
T10I4D100K_eclat['model_running_time']=T10I4D100K_eclat_time
```

```python
T10I4D100K_eclat.to_csv("T10I4D100K_eclat.csv",index=False)
```

### <font color='blue'> Eclat for T40I10D100K </font>

```python
T40I10D100K=[i.strip().split() for i in open("T40I10D100K.dat").readlines()]
```

```python
T40I10D100K=pd.DataFrame(T40I10D100K)
for i in range(len(T40I10D100K.columns)):
    T40I10D100K[i]=T40I10D100K[i].astype(str)+"_item"
    T40I10D100K[i].replace("None_item","None",inplace=True)
```

```python
T40I10D100K_relative_support=[0.3,0.5,1,1.5,2,2.5,3]
```

```python
T40I10D100K_eclat_time=[eclat_function(T40I10D100K, i) for i in T40I10D100K_relative_support]
```

```python
T40I10D100K_eclat=pd.DataFrame()
T40I10D100K_eclat["relative_support"]=T40I10D100K_relative_support
T40I10D100K_eclat['model_running_time']=T40I10D100K_eclat_time
```

```python
T40I10D100K_eclat.to_csv("T40I10D100K_eclat.csv",index=False)
```

### <font color='blue'> Eclat for  mushroom </font>

```python
mushroom=[i.strip().split() for i in open("mushroom.dat").readlines()]
```

```python
mushroom=pd.DataFrame(mushroom)
for i in range(len(mushroom.columns)):
    mushroom[i]=mushroom[i].astype(str)+"_item"
    mushroom[i].replace("None_item","None",inplace=True)
```

```python
mushroom_relative_support=[4,7,10,13,16,20]
```

```python
mushroom_eclat_time=[eclat_function(mushroom, i) for i in mushroom_relative_support]
```

```python
mushroom_eclat=pd.DataFrame()
mushroom_eclat["relative_support"]=mushroom_relative_support
mushroom_eclat['model_running_time']=mushroom_eclat_time
```

```python
mushroom_eclat.to_csv("mushroom_eclat.csv",index=False)
```

```python

```
