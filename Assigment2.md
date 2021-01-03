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

<!-- #region hideCode=false hidePrompt=false -->
## <font color ='blue'> Import library </font>
<!-- #endregion -->

```python hideCode=false hidePrompt=false
import pandas as pd
from skrules import SkopeRules
from sklearn.model_selection import cross_val_score
from sklearn.model_selection import cross_validate
import warnings
warnings.filterwarnings("ignore")
from sklearn.naive_bayes import GaussianNB
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import recall_score
```

<!-- #region hideCode=false hidePrompt=false -->
### <font color='blue'> Read the data </font>
<!-- #endregion -->

```python hideCode=false hidePrompt=false
train=pd.read_csv("../../data_min/train.csv")
test=pd.read_csv("../../data_min/test.csv")
```

<!-- #region hideCode=false hidePrompt=false -->
### <font color='blue'> Rename the values in class</font>
<!-- #endregion -->

```python hideCode=false hidePrompt=false
train.info()
```

```python hideCode=false hidePrompt=false
test.info()
```

```python hideCode=false hidePrompt=false
train.columns
```

```python hideCode=false hidePrompt=false
train_col=[ 'Pclass', 'Sex', 'SibSp','Parch', 'Embarked','Survived']
```

```python hideCode=false hidePrompt=false
test_col=['Pclass', 'Sex', 'SibSp','Parch', 'Embarked']
```

```python
feature=['Pclass', 'Sex', 'SibSp','Parch', 'Embarked']
```

```python hideCode=false hidePrompt=false
train[train_col].dropna(axis = 0).info()
```

```python hideCode=false hidePrompt=false
test[test_col].info()
```

### <font color="blue"> Lablel encoding for categorical variable </font>

```python
le_sex = preprocessing.LabelEncoder()
le_Embarked = preprocessing.LabelEncoder()
```

```python
train["Sex"]=le_sex.fit_transform(train["Sex"].astype('str') )
test["Sex"]=le_sex.transform(test["Sex"].astype('str') )

train["Embarked"]=le_Embarked.fit_transform(train["Embarked"].astype('str') )
test["Embarked"]=le_Embarked.transform(test["Embarked"].astype('str') )
```

```python
test_processed=test[test_col]
train_processed=train[train_col].dropna(axis = 0)
```

```python
test_processed.info()
```

```python
train_processed.info()
```

### <font color='blue'> Classification K(10) fold cross validation </font>
#### <font color='blue'> Random forest </font>

```python
rclf=RandomForestClassifier()
```

```python
scoring = ['precision_macro', 'recall_macro','f1_macro']
scores = cross_validate(rclf, train_processed.iloc[:,:-1],train_processed.iloc[:,-1], scoring=scoring, cv=10)
```

```python
scores=pd.DataFrame(scores)
```

```python
scores
```

#### <font color='blue'> Naive Bayes classifier </font>

```python
gnb = GaussianNB()
```

```python
scoring = ['precision_macro', 'recall_macro','f1_macro']
scores = cross_validate(gnb, train_processed.iloc[:,:-1],train_processed.iloc[:,-1], scoring=scoring, cv=10)
```

```python
scores=pd.DataFrame(scores)
```

```python
scores
```

#### <font color= 'blue' > Skope Rule Classifier </font>

```python
clf = SkopeRules(max_depth_duplication=None,
                 n_estimators=30,
                 precision_min=0.2,
                 recall_min=0.01,
                 feature_names=feature)
```

```python
scoring = ['precision_macro', 'recall_macro','f1_macro']
scores = cross_validate(clf, train_processed.iloc[:,:-1],train_processed.iloc[:,-1], scoring=scoring, cv=10)
```

```python
scores=pd.DataFrame(scores)
```

```python
scores
```

### <font color='blue'> Train the classifier on full training set for making submition </font>
#### <font color='blue'> Random forest </font>

```python
rclf=RandomForestClassifier()
```

```python
rclf.fit(train_processed.iloc[:,:-1],train_processed.iloc[:,-1])
```

```python
prediction=rclf.predict(test_processed)
```

```python
radnomforest_prediction=pd.DataFrame()
radnomforest_prediction["PassengerId"]=test["PassengerId"]
radnomforest_prediction["Survived"]=prediction
```

```python
radnomforest_prediction.head()
```

```python
radnomforest_prediction.tail()
```

```python
radnomforest_prediction.to_csv("../../data_min/radnomforest_prediction.csv",index=False)
```

### <font color= "blue" > Naive Bayes classifier </font>

```python
gnb = GaussianNB()
```

```python
gnb.fit(train_processed.iloc[:,:-1],train_processed.iloc[:,-1])
```

```python
nb_prediction=gnb.predict(test_processed)
```

```python
naive_bayes_prediction=pd.DataFrame()
naive_bayes_prediction["PassengerId"]=test["PassengerId"]
naive_bayes_prediction["Survived"]=nb_prediction
```

```python
naive_bayes_prediction.head()
```

```python
naive_bayes_prediction.tail()
```

```python
naive_bayes_prediction.to_csv("../../data_min/naive_bayes_prediction.csv",index=False)
```

#### <font color= 'blue' > Skope Rule Classifier </font>

```python
clf = SkopeRules(max_depth_duplication=None,
                 n_estimators=30,
                 precision_min=0.2,
                 recall_min=0.01,
                 feature_names=feature)
```

```python
clf.fit(train_processed.iloc[:,:-1],train_processed.iloc[:,-1])
```

```python
sr_prediction=clf.predict(test_processed)
```

```python
skope_rule_prediction=pd.DataFrame()
skope_rule_prediction["PassengerId"]=test["PassengerId"]
skope_rule_prediction["Survived"]=sr_prediction
```

```python
skope_rule_prediction.to_csv("../../data_min/skope_rule_prediction.csv",index=False)
```
