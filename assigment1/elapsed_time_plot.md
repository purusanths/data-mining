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

### <font color= "blue"> Import Library </font>

```python
import pandas as pd
import matplotlib.pyplot as plt
import warnings
import numpy as np
warnings.filterwarnings("ignore")
```

### <font color="blue"> Read the data </font>

```python
T10I4D100K_eclat=pd.read_csv("T10I4D100K_eclat.csv")
T10I4D100K_apriori=pd.read_csv("T10I4D100K_apriori.csv")
T10I4D100K_fpgrowth=pd.read_csv("T10I4D100K_fpgrowth.csv")

T40I10D100K_eclat=pd.read_csv("T40I10D100K_eclat.csv")
T40I10D100K_apriori=pd.read_csv("T40I10D100K_apriori.csv")
T40I10D100K_fpgrowth=pd.read_csv("T40I10D100K_fpgrowth.csv")

mushroom_eclat=pd.read_csv("mushroom_eclat.csv")
mushroom_apriori=pd.read_csv("mushroom_apriori.csv")
mushroom_fpgrowth=pd.read_csv("mushroom_fpgrowth.csv")

```

### <font color='blue'> Elapsed time plots </font>

```python
plt.plot(T10I4D100K_eclat["relative_support"], np.log(T10I4D100K_eclat["model_running_time"]), label = "Eclat")
plt.plot(T10I4D100K_apriori["relative_support"], np.log(T10I4D100K_apriori["model_running_time"]), label = "apriori")
plt.plot(T10I4D100K_fpgrowth["relative_support"], np.log(T10I4D100K_fpgrowth["model_running_time"]), label = "fpgrowth")
plt.title("Elapsed time for T10I4D100K data")
plt.legend(loc="upper left")
plt.show()

```

```python
plt.plot(T40I10D100K_eclat["relative_support"], np.log(T40I10D100K_eclat["model_running_time"]), label = "Eclat")
plt.plot(T40I10D100K_apriori["relative_support"], np.log(T40I10D100K_apriori["model_running_time"]), label = "apriori")
plt.plot(T40I10D100K_fpgrowth["relative_support"], np.log(T40I10D100K_fpgrowth["model_running_time"]), label = "fpgrowth")
plt.title("Elapsed time for T40I10D100K data")
plt.legend(loc="upper left")
plt.show()
```

```python
plt.plot(mushroom_eclat["relative_support"], np.log(mushroom_eclat["model_running_time"]), label = "Eclat")
plt.plot(mushroom_apriori["relative_support"], np.log(mushroom_apriori["model_running_time"]), label = "apriori")
plt.plot(mushroom_fpgrowth["relative_support"], np.log(mushroom_fpgrowth["model_running_time"]), label = "fpgrowth")
plt.title("Elapsed time for mushroomdata")
plt.legend(loc="upper left")
plt.show()

```

```python

```
