## INTRO
Social network analysis 是一種用很多relational methods 去了解和辨識節點之間的關係。其關係分為Symmetric（均勻對稱）or Asymmetric relationships。舉例：家族譜（對稱）、食物鏈（不對稱）。
#### 準確的可以將其定義為 Ｇ = ( V , A ) 
- V : 一個由 nodes、points或vertices組成的集合。
- A : 一個包含所有V之中任意兩點的間的關係，稱為arcs、arrows、directed edge，的集合。
Graph Theory 中定義的 Network 為有向圖，其關係具有權重。<br><br>
<img src="https://raw.githubusercontent.com/YuTe-Lai/Study_process/master/img/SNA_00.png"  width="600" height="277"><br>

## REPRESENTING SOCIAL NETWORK DATA
兩種方法表示SNA，畫出關係圖或是使用矩陣。<br>
<img src="https://raw.githubusercontent.com/YuTe-Lai/Study_process/master/img/SNA_01.png"  width="700" height="222"><br>
其中：
- Adjacency Matrix : The simplest and most common type of matrix is binary.It is extremely useful to conduct various formal analyses of graphs. 
<br>
<img src="https://raw.githubusercontent.com/YuTe-Lai/Study_process/master/img/SNA_02.png"  width="600" height="277"><br>

## TYPES OF NETWORK DATA
### Egocentered Networks : 
Data on a respondent (ego) and the people they are connected to.<br>
Measures : Size、Types of relations
<br>
<img src="https://raw.githubusercontent.com/YuTe-Lai/Study_process/master/img/SNA_03.png"  width="600" height="277"><br>

### Complete Networks : 
All members of a population are connected. All actors are within a particular boundary. Due to the missing data, there are never exactly complete without setting boundary.<br>
Measures : Graph properties、Density、Sub-groups、Positions
<br>
<img src="https://raw.githubusercontent.com/YuTe-Lai/Study_process/master/img/SNA_04.png"  width="390" height="420"><br>
