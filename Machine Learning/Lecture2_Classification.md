# Classification vs Regression
監督是學習的整體過程可以簡單的視為: 輸入特徵(input)，給定答案(output)，透過機器去找出兩者之間的關係(function)，在未來便能依據兩者之間的關係做出預測。<br>
在監督式學習中，如果是預測連續的值（例如：預測未來股價、預測回購機率...等），便是迴歸（Regression）。
而如果預測的值是不連續的項目種類(例如：是否回購、是否續租...等)，則是分類(classification)。<br>
<img src="https://github.com/YuTe-Lai/Study_process/blob/master/Machine%20Learning/img/Lecture2_classification_vs_regression.png?raw=true" alt="R"  width="660" height="320"><br>

# K-NN 演算法
### 使用鳶尾花卉數據集
```python
#匯入資料集
from sklearn import datasets
iris = datasets.load_iris()

#整理資料集
import pandas as pd
features = pd.DataFrame(iris['data'], columns = iris['feature_names'])
targets = pd.DataFrame(iris['target'], columns = ['class'])
df = pd.concat([features, targets], axis=1)

#繪出資料
import matplotlib.pyplot as plt
import seaborn as sns
plt.style.use('ggplot')
g = sns.FacetGrid(df, hue='class', size = 5)
g.map(plt.scatter,'sepal length (cm)','sepal width (cm)')#花萼長vs寬
g.add_legend()

```
<img src="https://github.com/YuTe-Lai/Study_process/blob/master/Machine%20Learning/img/Lecture2_classification_KNN_df_graph.png?raw=true"  width="380" height="320"><br>

```python
#分割訓練、測試資料
import numpy as np
from sklearn.model_selection import train_test_split
x = df.iloc[:,:-1].values
y = df.iloc[:,4].values
x_train,x_test,_y_train,y_test = train_test_split(x,y,test_size = 0.33,random_state = 1)

# KNN 訓練模型
from sklearn.neighbors import KNeighborsClassifier
knn = KNeighborsClassifier(n_neighbors=3) # k=3
knn.fit(x_train, y_train)
pred = knn.predict(x_test)

# 計算正確率
from sklearn.metrics import accuracy_score
print('正確率：'accuracy_score(y_test, pred))
```
正確率：0.98<br>

```python
#調整參數＆評估結果
from sklearn.model_selection import cross_val_score
scores = cross_val_score(knn, x_train, y_train, cv=10, scoring = 'accuracy')
```




