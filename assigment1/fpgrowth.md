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

### <font color='blue'> Import library </font>

```python
import pandas as pd
from mlxtend.preprocessing import TransactionEncoder
from mlxtend.frequent_patterns import fpgrowth
import time
```

### <font color='blue'> Fp growth function </font>

```python
def fp_growth_function(dataset,min_support):
    te = TransactionEncoder()
    te_ary = te.fit(dataset).transform(dataset)
    df = pd.DataFrame(te_ary, columns=te.columns_)
    start = time.process_time()
    fpgrowth(df, min_support=min_support/100, use_colnames=True)
    elapsed_time_secs = time.time() - start
    return elapsed_time_secs

```

### <font color='blue'> Fpgrowth for T10I4D100K </font>

```python
T10I4D100K = [i.strip().split() for i in open("T10I4D100K.dat").readlines()]
```

```python
T10I4D100K_relative_support=[0.3,0.5,1,1.5,2,2.5,3]
```

```python
T10I4D100K_fpgrowth_time=[fp_growth_function(T10I4D100K, i) for i in T10I4D100K_relative_support]
```

```python
T10I4D100K_fpgrowth=pd.DataFrame()
T10I4D100K_fpgrowth["relative_support"]=T10I4D100K_relative_support
T10I4D100K_fpgrowth['model_running_time']=T10I4D100K_fpgrowth_time
```

```python
T10I4D100K_fpgrowth.to_csv("T10I4D100K_fpgrowth.csv",index=False)
```

### <font color='blue'> fpgrowth for T40I10D100K </font>

```python
T40I10D100K=[i.strip().split() for i in open("T40I10D100K.dat").readlines()]
```

```python
T40I10D100K_relative_support=[0.3,0.5,1,1.5,2,2.5,3]
```

```python
T40I10D100K_fpgrowth_time=[fp_growth_function(T40I10D100K, i) for i in T40I10D100K_relative_support]
```

```python
T40I10D100K_fpgrowth=pd.DataFrame()
T40I10D100K_fpgrowth["relative_support"]=T40I10D100K_relative_support
T40I10D100K_fpgrowth['model_running_time']=T40I10D100K_fpgrowth_time
```

```python
T40I10D100K_fpgrowth.to_csv("T40I10D100K_fpgrowth.csv",index=False)
```

### <font color='blue'> fpgrowth for  mushroom </font>

```python
mushroom=[i.strip().split() for i in open("mushroom.dat").readlines()]
```

```python
mushroom_relative_support=[4,7,10,13,16,20]
```

```python
mushroom_fpgrowth_time=[fp_growth_function(mushroom, i) for i in mushroom_relative_support]
```

```python
mushroom_fpgrowth=pd.DataFrame()
mushroom_fpgrowth["relative_support"]=mushroom_relative_support
mushroom_fpgrowth['model_running_time']=mushroom_fpgrowth_time
```

```python
mushroom_fpgrowth.to_csv("mushroom_fpgrowth.csv",index=False)
```
