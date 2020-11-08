# 資料結構
## 陣列 Array
陣列（如下）是有序串列的一種方式，其佔用連續的記憶體空間，各元素型態（Type）皆需相同，其支援循序存取（Sequential）及 隨機存取（Random Access）。<br>
`[1,3,5,7,9]`、`['a','b','c','d','e']`<br>
但陣列在插入、刪除元素較為麻煩：需移動其它元素，不易動態增加或刪減空間大小。<br>
insert（4）：`[1,3,5,7,9]`->`[1,3, ,5,7,9]`->`[1,3,4,5,7,9]`<br>
## 鏈結串列 Link Lists
Link List由一組節點 (Node) 依照順序串列所組成的，僅支援 Sequential Access，每個Node除了有Data欄之外，必須有≥ 1 個Link欄(或稱Pointer)，用以指向下一個Node的位址，而最後一個節點的pointer將會指向null。<br>
```python
#Single link list中的每個節點只有指向下一個Node，沒有指出上一個Node，相對於有指出上一個Node的double link list。

class SingleLinkList:
    def __init__(self):
        self.head = None
        self.tail = None
        return
```
各Node不用佔用連續的記憶體空間，每個Node的資料型態 (Data Type) 不一定要相同。<br>
```python
class ListNode:
  def __init__(self, data): 
    self.data = data    #儲存資料
    self.next = None    #儲存pointer
    return
```
在建立list的一開始，我們預設裡面是沒有節點（Node）的。而link list本身帶有head跟tail兩個屬性。所以當我們加入一個新的節點時：<br>
- 若list本身還沒有任何節點，則head以及tail都會變成新的結點。<br>
- 若list已經包含有其他節點，則新加入的節點變成新的tail（本來的tail指向新的節點）。

```python
def add_list_item(self,item):
    if not isinstance(item, ListNode):  #確認輸入item為node型態
        item = ListNode(item)           #不是的話將它改為node型態
    if self.head is None:               #若list本身還沒有任何節點，則head以及tail都會變成新的結點。
        self.head = item  
    else:
        self.tail.next = item           #若list已經包含有其他節點，則新加入的節點變成新的tail。
    self.tail = item
    return
```
Link List可以輕鬆的插入、刪除Node，只要改變Node之中的Pointer就可以了。<br>
### Insert:
將資料item插入在串列list中的節點x 之後。<br>
<img src="https://github.com/YuTe-Lai/yute-lai.github.io/blob/master/img/DS_linklist_insert.png?raw=true" alt="Link List_Insert"  width="600" height="200"><br>
```python
class Linklist:
    def insert(self,prev_node, insert_data):
#確認前一個node存不存在
        if prev_node is None:  
            print("The previous node must in LinkedList!")
            return
#將要插入的Data存成Node
        new_node = Node(insert_data) 
#用new_node.next取代prev_node.next
        new_node.next = prev_node.next
#把prev_node.next指向new_node
        prev_node.next = new_node
```
### Delete:
刪除Link List的節點時，會先改變串列的指標，以做到邏輯性移除(Logically Remove)的動作，再將被移除的節點做實際刪除（從記憶體中刪除）。<br>
<img src="https://github.com/YuTe-Lai/yute-lai.github.io/blob/master/img/DS_linklist_delete.png?raw=true" alt="Link List_Delete"  width="600" height="320"><br>
```python
class Linklist:
    def delete(self, key):
        #先將head暫存起來  
        temp = self.head  
        #確認head不為空
        if (temp is not None):  
            #CASE1：若要刪除第一個node
            if (temp.data == key):  
                #用第二個node取代head
                self.head = temp.next
                #從記憶體中刪除
                temp = None
                return
  
        #從head開始搜尋要刪除的目標key
        while(temp is not None):  
            if temp.data == key:  
                break
            
            prev = temp  
            temp = temp.next
  
        #如果key不在LinkList裡  
        if(temp == None):  
            return
  
        #將key node從Link List裡取出
        prev.next = temp.next
        #從記憶體中刪除
        temp = None
```
### 其他Link List種類
#### Double Link List:
串列中各節點除了Data欄之外，另外有2 個Link欄，用以指向前一個與下一個節點之位址。<br>
<img src="https://github.com/YuTe-Lai/yute-lai.github.io/blob/master/img/DS_Double_linklist.png?raw=true" alt="Double Link List"  width="666" height="230"><br>

#### Circularly Link List:
將Single Link List中，最後一個node的指標指回第一個node。<br>
<img src="https://github.com/YuTe-Lai/yute-lai.github.io/blob/master/img/DS_Circularly_linklist.png?raw=true" alt="Circularly Link List"  width="666" height="230"><br>

## 樹 Tree
樹是由1個以上的Nodes所組成的有限集合，其必須滿足：<br>
- 至少有一個節點（Node）稱為根（Root）。<br>
- 剩下的Nodes可以分成T1、T2、...、Tn個互斥集合，稱為子集合（Subtree）。<br>
<img src="https://github.com/YuTe-Lai/yute-lai.github.io/blob/master/img/Tree.png?raw=true" alt="tree"  width="500" height="280"><br>
樹中的節點有分成以下幾種：<br>
- 葉子（Leaf）:分枝度為0（沒有子集合）的節點。<br>
- 非葉子（Non-Leaf Node、Non-Terminal Node、Internal Node）：樹中所有非葉子的節點，或是Degree >= 1的節點。<br>
- 父節點（Parent Node）：若一個節點x後有後繼結點（Successor Node），則x為父節點。整顆樹的樹根為全部集合的父節點。<br>
- 子節點（Child Node）：若一個節點y前有前輩結點（Predecessor Node），則y為子節點。某節點的所有子樹（Subtree）的樹根為該節點的子節點。<br>
- 兄弟（Sibling）：同一個父節點的所有子節點互稱為Sibling。<br>
- 祖先（Ancestor）：從樹根到某一節點所經過的所有節點，稱為該節點的Ancestor，通常為一集合`Ancestor of C:{ A、B }`。<br>
#### 平衡因子 Balance Factor：
在一個Binary Tree中，`H(左)-H(右)`代表一個節點的平衡因子。其中H(左)和H(右)分別代表左、右子集合的高度。對一顆AVL高度平衡樹裡的任一節點來說`Balance_Factor(Node)=1、-1、0`等三種情況。

### 二元樹 Binary Tree：
Binary Tree為擁有不小於0個Nodes的所構成的有限集合，意思就是他可以是一顆空的或非空的樹，若不為空，則需要Root及左、右子集合。<br>
- 二元樹中，第i個Level的node個數最多有`2^(i-1)`個。
- 高度為H的二元樹中，其node個數最多有`2^H -1`個。
- 非空的二元樹中，若leaf個數為n個，分枝度（degree）為2的node個數為m個，則`n=m+1`。
<br>

#### 具有最多Node個數的二元樹稱為：Full Binary Tree 
- 所有leaf nodes具有相同的level(或相同的height)
- 所有非leaf的nodes都有兩個subtree
- 高度為H，其Node個數必為`2^H -1`
- Full B.T 下具有n個Node，其高度必為`log2(n+1)`
#### 若一棵樹的node按照Full Binary Tree的次序排列(由上至下，由左至右)，則稱此樹為：Complete Binary Tree
下圖中的樹共有11個node，但是第11個node(K)應該要是第5個node(E)的child，因此，此樹並非Complete Binary Tree。
<img src="https://github.com/YuTe-Lai/yute-lai.github.io/blob/master/img/DS_Complete_binary_tree.png?raw=true" alt="complete binary tree"  width="420" height="300"><br>

### 二元搜尋樹 Binary Search Tree：
二元搜尋樹常應用於排序（Sort）或搜尋（Search）。其定義與二元樹（Binary Tree）一樣，不過二元搜尋樹如果不為空除了需要Root及左、右子集合外，還需滿足左子集合中所有node鍵值均小於Root，右子集合亦然。


### Tracing Tree

```python
class TreeNode(object):
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

class solution(object):
    def insert(self, root, key):
        if root is None:
            root = TreeNode(key)
            return root
        else:
            if key > root.val:
                root.right = self.insert(root.right,key)
            else:
                root.left = self.insert(root.left,key)
            return root

    def search(self, root, key):
        if root is None :
            return False
        elif root.val == key:
            return True
        elif key > root.val:
            return self.search(root.right,key)
        elif key < root.val:
            return self.search(root.left,key)

    def inorder(self,root): 
        if root: 
            self.inorder(root.left) 
            print(root.val) 
            self.inorder(root.right) 
           
    def findmin(self,root):
        while root.left is not None:
            root = root.left
        return root
    
    def delete(self,root,key):
        if root is None:
            return False
        elif key > root.val:
            root.right = self.delete(root.right, key)
        elif key < root.val:
            root.left = self.delete(root.left, key)
        else:   
            if root.left is None:
                replace = root.right  
                root = None            
                return replace         
            elif root.right is None:  
                replace = root.left
                root = None
                return replace
            else:  
                replace = self.findmin(root.right) 
                root.key = replace.key 
                root.right = self.delete(root.right,replace.key)
            return root
```

## 堆疊 Stack
堆疊是具有LIFO (last in-first out)或FILO (first in-last out) 性質的有序串列。其插入元素的動作稱為Push, 刪除元素的動作稱為Pop。而Push/Pop的動作皆發生在同一端，此端稱為Top。<br>
<img src="https://github.com/YuTe-Lai/yute-lai.github.io/blob/master/img/DS_Stack.png?raw=true" alt="Stack"  width="666" height="266"><br>
### 堆疊的應用:電腦四則運算
#### 中序式
一般的算式，主要是將運算元（數字）放在運算子（符號）的兩旁，例如a+b/d這樣的式子，這稱之為中序（Infix）表示式，對於人類來說，這樣的式子很容易理解，但由於電腦執行指令時是有順序的，遇到中序表示式時，無法直接進行運算，而必須進一步判斷運算的先後順序，所以必須將中序表示式轉換為另一種表示方法。
#### 前序式
後序（Postfix）表示式，又稱為逆向波蘭表示式（Reverse polish notation），例如`(a+b)*(c+d)`這個式子，表示為後序表示式時是`ab+cd+*`。
#### 後序式
前序（Prefix）表示式，波蘭表示式（Polish notation），例如剛剛`(a+b)*(c+d)`的式子，表示為前序表示式為`*+ab+cd`。
#### 運算式的轉換
由中序表示法轉換成前/後序表示法的方法有兩種：<br>
- 加括號去除法：這種方法是人類使用的方法，將運算子兩旁的運算元依先後順序全括號起來，然後將所有的右括號取代為左邊最接近的運算子（從最內層括號開始），最後去掉所有的左括號就可以完成後序表示式。
例如：<br>
`a+b*d+c/d`   =>    `((a+(b*d))+(c/d))` -> `abd*+cd/+`

- 堆疊處理法：由左而右掃描資料，依據資料是運算元或運算子作不同的處理，運算子還要考慮其優先次序。直接敘述演算法的話就是使用迴圈，取出中序式的字元，遇到運算元直接輸出；堆疊運算子與左括號；堆疊中運算子優先順序若大於等於讀入的運算子優先順序的話，直接輸出堆疊中的運算子，再將讀入的運算子置入堆疊；遇右括號輸出堆疊中的運算子至左括號。<br>

<img src="https://github.com/YuTe-Lai/yute-lai.github.io/blob/master/img/DS_Stack_caculate.png?raw=true" alt="By Stack" width="326" height="411">

## 佇列 Queue
Queue是具有FIFO(First-In-First-Out)或LILO(Last-In-Last-Out)的資料結構，就像排隊買票的隊伍即可視為Queue，先進入隊伍的人，可以優先買票離開隊伍，而後到的人，就需要等隊伍前面的人都買完票後才能買。<br>
如同普遍認知的排隊隊伍，Queue也具有以下特徵：<br>
- 隊伍有前方(以front表示)以及後方(以rear表示)之分。
- 若要進入隊伍(Push)，一定是從rear(back)進入。把資料從Queue的「後面」放進Queue，並更新成新的rear。
- 若要離開隊伍(Pop)，一定是從front離開。把front所指向的資料從Queue中移除，並更新front。
<img src="https://github.com/YuTe-Lai/yute-lai.github.io/blob/master/img/DS_Queue.png?raw=true" alt="Queue" width="666" height="196"><br>
一般的Queue，會有以下幾個處理資料結構的功能：<br>
- getFront：回傳front所指向的資料。
- getBack：回傳rear所指向的資料。
- IsEmpty：確認Queue裡是否有資料。
- getSize：回傳Queue裡的資料個數。

















# 演算法
演算法是一個有輸入跟輸出的解決問題的流程，它具有明確、有限步驟且有效的特性，常用於計算、資料處理和自動推理。通常在針對某一問題開發程式時，都會經過下列流程：<br>
## Step 1：明確定義問題
理論上來說，演算法可以解決大部分的問題，甚至要預測尚未發生的事情也並無不可能，但現實生活中的變數太多且難以量化，容易造成輸出結果不盡理想，故現階段在定義問題時建議可以先將問題簡單化。
<br>
## Step 2：設計演算法
### 演算法的定義：
高德納(Donald Ervin Knuth) 在《電腦程式設計藝術》裡歸納出一個演算法需要俱備的五個特性：<br>
- 輸入：一個演算法必須有0或多個輸入<br>
- 輸出：一個演算法應至少有一個或以上的輸出結果（ 有可能是 0 或是 null ）<br>
- 明確性：演算法的每個指令或步驟描述必須明確，以保證演算法的實際執行結果是確實符合要求<br>
- 有限性：在有限步驟後一定會結束，不會進入無窮迴圈<br>
- 有效性：又稱可行性。演算法中描述的步驟都是可以運算的<br>
<br>
而怎麼樣才能設計一個符合定義的演算法呢？常見的方法有兩種： **流程圖** 、 **虛擬碼** 。

<img src="https://github.com/YuTe-Lai/yute-lai.github.io/blob/master/img/flowchart.png?raw=true" alt="flowchart"  width="350" height="300">

<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;流程圖
<img src="https://github.com/YuTe-Lai/yute-lai.github.io/blob/master/img/virtualcode.png?raw=true" alt="virtualcode"  width="350" height="300">
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;虛擬碼<br>
<br>

## Step 3：計算其執行時間及所使用的記憶體空間大小 
### 時間複雜度：
簡單的定義就是電腦執行演算法所需要耗費的時間成本。但因為每台電腦的計算能力不一樣，所以常用"演算法執行需要幾個指令"來做計算（忽略每個指令需要的時間）。T(n)：表示當輸入資料量為 n 時，演算法中所有指令所需的實際執行次數。
<br>
<img src="https://github.com/YuTe-Lai/yute-lai.github.io/blob/master/img/T(n).png?raw=true" alt="Big-O Complexity Chart"  width="650" height="420"><br>
時間複雜度會運用**漸近符號** asymptotic notation來表示，在這邊**漸近符號** asymptotic notation主要有兩種表示方法：<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Big-Ｏ(O) : 某演算法時間函數的即上限 (Upperbound)，演算法在執行時所花費的時間成長，最差的情況不會超過它。通常會使用**概量**表示。**概量**：當 f(n) = n^2 + 3n 這個函數，當 n 很大時，3n 會比 n^2 小很多，則可以忽略不計。當 n 趨近無限大時，f(n) 等價於 n^2 。<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Omega(Ω)：某演算法時間函數的下限 (Lower bound)，演算法在執行時所花費的時間成長，最好的情況也不會低於它。<br>
<br>
通常我們使用 ` Big Ｏ notation `大Ｏ符號來表示時間複雜度。假設我們將其時間複雜度表示為`Ｏ(T(n))`，則其中`T(n)` 又稱為**執行時間的成長率**，是影響速度最大的變數。<br>
下面為`Ｏ(1)`的例子，這個演算法執行的步驟是固定的，跟輸入的值無關（不管num輸入多少，程式皆只會執行一次）：

```python
# 不管 n 輸入為多少，這個程式永遠只會執行一次
def print_num(num):
    print(num)
```
下面是`Ｏ(n)`的例子，時間複雜度跟輸入的次數有關：隨著 num 改變，需要跑 num 次，是線性時間的成長。這邊 `T(n)` 等於 `n`，所以 `Ｏ(T(n))` 就是 `Ｏ(n)`。
```python
def sum_number(num):
    total = 0
    for n in num:
        total += num
    return total

sum_number(10)
```
<img src="https://github.com/YuTe-Lai/yute-lai.github.io/blob/master/img/Big_O_complexity_chart.png?raw=true" alt="Big-O Complexity Chart"  width="800" height="600">

### 空間複雜度：
空間複雜度是指演算法所需要消耗的記憶體資源。其計算和表示方法與時間複雜度類似，一般也都用**概量**（asymptotic analysis）來表示。<br>
如剛剛數字加總的例子，不管程式跑了多少遍，使用的變數數量都只有`total`一個，故該函式的空間複雜度為 Ｏ(1)：
```python
def sum_number(num):
    total = 0
    for n in num:
        total += num
    return total

sum_number(10)
```

<br>
## Step 4：撰寫程式

<br>



參考資料：https://blog.techbridge.cc/2019/03/01/computer-science-algorithm-introduction/
## QuickSort

```python
def quick_sort(list): #extra-place
    smaller = []
    bigger = []
    keylist = []
    if len(list) <= 1:
        return list
    else:
        key = list[0] #第一個數為key值
        for i in list:
            if i < key: #比key值小的數
                smaller.append(i)
            elif i > key: #比key值大的數
                bigger.append(i)
            else:
                keylist.append(i)
    smaller = quick_sort(smaller)
    bigger = quick_sort(bigger)
    return smaller + keylist + bigger
```


## HeapSort

```python
def swap(g, h):                    
    arr[g], arr[h] = arr[g], arr[h] 

def heapify(n,i):   
    l=2 * i + 1  
    r=2 * (i + 1)   
    max=i   
    if l < n and arr[i] < arr[l]:   
        max = l   
    if r < n and arr[max] < arr[r]:   
        max = r   
    if max != i:   
        swap(i, max)   
        heapify(n, max)   

def heap_sort():     
    n = len(arr)   
    s = n // 2 - 1 
    for i in range(s, -1, -1):   
        heapify(n, i)   
    for i in range(n-1, 0, -1):   
        swap(i, 0)   
        heapify(i, 0) 
```

## MergeSort

```python
def merge_sort(arr):
    if len(arr)<=1:   
        return arr
    else:
        mid = len(arr)//2 
        left = arr[:mid] 
        right = arr[mid:]
        l_arr = merge_sort(left)      
        r_arr = merge_sort(right)
        return merge(l_arr,r_arr)

    
def merge(l_arr,r_arr):
    final = []
    while l_arr and r_arr:
        if l_arr[0] < r_arr[0]:
            
            final.append(l_arr[0])
            del l_arr[0]

        else:
            final.append(r_arr[0])
            del r_arr[0]
            
    final = final + l_arr + r_arr
    return final

```

## HashTable
```python
from Crypto.Hash import MD5

class ListNode:
    def __init__(self, val):
        self.val = val
        self.next = None

        
class MyHashSet:
    def __init__(self, capacity=5):
        self.capacity = capacity
        self.data = [None] * capacity

        
    def add(self, key):
        h = MD5.new()
        h.update(key.encode("UTF-8"))
        arr = int(h.hexdigest() , 16)%self.capacity
        if self.data[arr] is None:
            self.data[arr] = ListNode(h)        
        else:
            n = ListNode(h)
            o = self.data[arr]
            while o.next is not None:
                o = o.next
            o.next = n
        
        
        
        
    def remove(self, key):
        h = MD5.new()
        h.update(key.encode("UTF-8"))
        arr = int(h.hexdigest() , 16)%self.capacity
        brr = int(h.hexdigest() , 16)
        n = self.data[arr]
        if self.data[arr]:
            cur = n
            while n.val != brr and n.next:
                n = n.next  
            cur.next = n.next
        else:
            return

        

        
    def contains(self, key):
        h = MD5.new()
        h.update(key.encode("UTF-8"))
        arr = int(h.hexdigest() , 16)% self.capacity
        brr = int(h.hexdigest() , 16)
        head = self.data[arr]
        if head is None:
            return False
        else:
            while head.val != brr:
                head = head.next
                if head is None: 
                    return False
            return True           
```

## BFS & DFS
```python

from collections import defaultdict
  

class Graph:

    def __init__(self): 
        self.graph = defaultdict(list) 

    def addEdge(self,u,v): 
        self.graph[u].append(v) 
  

    def BFS(self, s):
        visited = [0] * (len(self.graph)) 
        que = [] 
        que.append(s) 
        visited[s] = 1 
        while que:
            s = que.pop(0)
            print(s, end=',')
            for i in self.graph[s]:
                if visited[i] == 0:
                    que.append(i)
                    visited[i] = 1
                    

    def DFS(self, s):
        stack = []
        a=[]
        a.append(s) #直接把根放進去
        while len(a) != len(self.graph):
            for i in self.graph[s]:
                if i not in stack and i not in a:
                    stack.append(i)
            s=stack.pop(-1)
            a.append(s)
        return a

```
## Dijkstra & Kruskal

```python
from collections import defaultdict 

class Graph(): 

    def __init__(self, vertices): 
        self.v = vertices 
        self.graph = [] 
        self.graph_matrix = [[0 for column in range(vertices)]  
                    for row in range(vertices)] 
        
    def addEdge(self,u,v,w):
        self.graph.append([u,v,w]) 
        
    def Dijkstra(self, s):
        visited = [False] * self.v 
        dist = [99999] * self.v 
        dist[s] = 0
        for i in range(self.v):
            m = self.find_min(dist,visited,i)
            visited[m] = True
            for r in range(self.v):
                if self.graph[m][r] > 0 and  visited[r] == False and dist[r] > dist[m] + self.graph[m][r]:
                    dist[r] = dist[m] + self.graph[m][r]
        for node in range(self.v): 
            print (node, ":", dist[node])
                    
                 
    def find_min(self,dist,visited,root):
        min = 99999
        for v in range(self.v):
            if dist[v]<min and visited[v] == False:
                min = dist[v]
                min_index = v
        return min_index
        
                
            
    def Kruskal(self):
        h=0
        subset=set() 
        MST=[]
        self.graph =  sorted(self.graph,key=lambda item: item[2]) 
        
        for m in self.graph:
            t = set(m[:2]) 
            if t.issubset(subset) == False:
                subset.update(m[:2])
                MST.append(m)

        while h < len(MST):
            print(MST[h][0],"-",MST[h][1],":",MST[h][2])
            h = h+1
```

