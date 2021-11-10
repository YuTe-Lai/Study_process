## INTRO
Social network analysis 是一種用很多relational methods 去了解和辨識節點之間的關係。其關係分為Symmetric（均勻對稱）or Asymmetric relationships。舉例：家族譜（對稱）、食物鏈（不對稱）。
#### 準確的可以將其定義為 Ｇ = ( V , A ) 
- V (節點集合): 一個由 nodes、points或vertices組成的集合。
- A (鄰接矩陣): 一個包含所有V之中任意兩點的間的關係，稱為arcs、arrows、directed edge，的集合。
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
<img src="https://raw.githubusercontent.com/YuTe-Lai/Study_process/master/img/SNA_04.png"  width="390" height="400"><br>

## DISTANCE BETWEEN ACTORS
### Geodesic distance
The minimum number of edges that takes to go from one node to another.<br>
Multiple connections may indicate a stronger relation between two actors than a single connection.<br>
<img src="https://raw.githubusercontent.com/YuTe-Lai/Study_process/master/img/SNA_05.png"  width="555" height="222"><br>

### Eccentricity(偏心距)
An actor’s largest geodesic distance is called its eccentricity – a measure of how far an actor is from the furthest other.<br>
If two nodes are not reachable from each other (i.e. the network is disconnected), their geodesic distance is infinite.<br>
The ***diameter(直徑)*** of a network is the maximum eccentricity over all the actors of the network.( if the network is not connected the largest distance is infinity ).
The ***radius(半徑)*** of a network is the minimum eccentricity over all the actors of the network. <br>
Vertices with maximum eccentricity are called ***peripheral vertices(邊緣節點)***. Vertices of minimum eccentricity from the ***Centre(中心節點)***. <br>
diam(G) ≤ 2 rad(G)

### Walks
A walk is a sequence of nodes and relations that begins and ends with nodes. Walks are unrestricted. <br>
Closed walk is one where the beginning and end point of the walk are the same actor. The length of a walk is the number of edges that it uses. <br>
Some examples of walks between A and C in the graph represented in Figure :<br>
<img src="https://raw.githubusercontent.com/YuTe-Lai/Study_process/master/img/SNA_06.png"  width="588" height="222"><br>

### Cycles
A cycle is a closed walk of 3 or more actors, all of whom are distinct , except for the origin/destination actor.<br>
<img src="https://raw.githubusercontent.com/YuTe-Lai/Study_process/master/img/SNA_07.png"  width="500" height="222"><br>

### Trails
A trail between two actors is any walk that includes any given relation at most once. (The same actors, different edges, can be part of a trial multiple times).
<br>
<img src="https://raw.githubusercontent.com/YuTe-Lai/Study_process/master/img/SNA_08.png"  width="622" height="222"><br>

### Paths
A path is a walk in which each actor (and therefore  each  relation) in the graph may be used at most once. All paths are trails and walks, but not all walks and all trails are paths.<br>

### Compare walks, trails and paths
- 走道（ Walk ）：一連串的邊。可以重複經過同樣的點和邊，可以來來回回繞圈。
- 跡（ Trail ）：一條走道，沒有重複經過同樣的邊。
- 路徑（ Path ）：一條走道，沒有重複經過同樣的點（與邊）。
<br>
<img src="https://raw.githubusercontent.com/YuTe-Lai/Study_process/master/img/SNA_09.png"  width="600" height="222"><br>


## CENTRALITY AND POWER
中間度（ Centrality ）可以用來衡量節點們在網絡中的重要性。例如：在網路中這個人有多重要？這條馬路在城市中有多重要？
- 分支度（degree）: 給定一節點，其分支度為其相鄰節點的個數，即為其圖形的區域中心性（Local Centrality）。
- 接近度（closeness）: 以節點間的最短路徑來衡節點的全域中心性（Global Centrality）。
- 中介度（betweenness）: 加總節點k 位於任何兩節點i, j 之間所有可能最短路徑的比率，可得節點k 的中介中心性。












