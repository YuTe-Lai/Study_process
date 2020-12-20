# 決策樹 DecisionTree
決策樹模型是常用於解決分類問題的樹狀結構。決策樹由許多節點和有向分枝組成。
決策樹的決策過程是從根節點開始，將資料與決策樹中的內部節點（特徵節點）進行比較，並按照比較結果選擇分枝（欄位輸出結果），直到葉子節點（分類標記）後則為最終的決策結果。
- 每個內部節點代表一個評估欄位
- 每個分支代表一個可能的欄位輸出結果
- 每個樹葉節點代表不同的分類標記

<img src="https://github.com/YuTe-Lai/Study_process/blob/master/Machine%20Learning/img/Lecture4_DecisionTree_intro.png?raw=true" width="480" height="300"><br>

# 建立決策樹
### 不同類型的節點分割
- 二元屬性：<br>
二元屬性的資料分割後只會產生兩個分支。<br>

<img src="https://github.com/YuTe-Lai/Study_process/blob/master/Machine%20Learning/img/Lecture4_DecisionTree_branch1.png?raw=true" width="180" height="160"><br>

- 名目屬性：<br>
名目屬性的資料沒有前後順序關係，其可以分割出不同值域的分支，其分支也可以用子集合表示。<br>
<img src="https://github.com/YuTe-Lai/Study_process/blob/master/Machine%20Learning/img/Lecture4_DecisionTree_branch2.png?raw=true" width="470" height="290"><br>

- 順序屬性：<br>
順序屬性的資料有前後順序關係，可以產生二元或多元分割，其分支也可以用子集合表示，但每個子集必須沒有違反屬性質的順序。<br>
<img src="https://github.com/YuTe-Lai/Study_process/blob/master/Machine%20Learning/img/Lecture4_DecisionTree_branch3.png?raw=true" width="520" height="210"><br>

- 連續性屬性：<br>
可以採用離散化的方式將資料分割成二元或多元，但須保持資料的順序性。<br>
<img src="https://github.com/YuTe-Lai/Study_process/blob/master/Machine%20Learning/img/Lecture4_DecisionTree_branch4.png?raw=true" width="510" height="210"><br>

## 特徵選擇
特徵選擇就是從數據的特徵中選擇一個特徵作為當前節點的分割標準，那在分割的過程中，我們希望在下一個分支節點中的資料盡可能的屬於同一類，也就是要盡量讓熵值越小越好。<br>
<img src="https://github.com/YuTe-Lai/Study_process/blob/master/Machine%20Learning/img/Lecture4_DecisionTree_Entropy.png?raw=true" width="660" height="230"><br>


