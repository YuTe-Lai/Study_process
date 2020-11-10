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

#### 平衡因子 Balance Factor：
在一個Binary Tree中，`H(左)-H(右)`代表一個節點的平衡因子。其中H(左)和H(右)分別代表左、右子集合的高度。對一顆AVL高度平衡樹裡的任一節點來說`Balance_Factor(Node)=1、-1、0`等三種情況。
<br>

#### 二元樹追蹤 Tracing Tree
二元樹追蹤主要是拜訪樹中每個節點一次，而tracing有兩種方式：<br>
- 深度優先 Depth First：由根節點出發，沿著某一子樹由上到下垂直走訪到底，再回到上一個Level選擇其他子樹遞迴處理。
<img src="https://github.com/YuTe-Lai/yute-lai.github.io/blob/master/img/DS_Depth_first.png?raw=true" alt="Depth First"  width="420" height="300"><br>
- 廣度優先 Breadth First：由根節點出發，依水平方向由左到右，將同一Level處理完後再選擇下一個Level遞迴處理。
<img src="https://github.com/YuTe-Lai/yute-lai.github.io/blob/master/img/DS_Breadth_first.png?raw=true" alt="Breadth First"  width="420" height="300"><br>

### 二元搜尋樹 Binary Search Tree：
二元搜尋樹常應用於排序（Sort）或搜尋（Search）。其定義與二元樹（Binary Tree）一樣，不過二元搜尋樹如果不為空除了需要Root及左、右子集合外，還需滿足左子集合中所有node鍵值均小於Root，右子集合亦然。<br>
<img src="https://github.com/YuTe-Lai/yute-lai.github.io/blob/master/img/DS_Binary_search_tree.png?raw=true" alt="Binary Search Tree"  width="700" height="200"><br>

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
### 霍夫曼樹 Huffman Tree
霍夫曼樹(Huffman Tree)是二元搜尋樹的延伸應用，它是霍夫曼(D.A.Huffman)的編碼模式，在霍夫曼編碼當中將資料視為有權重的葉子，再將各資料依出現頻率及次數加以分類，構築出一個叫**霍夫曼樹**的樹狀資料結構，然後再加以分配資料的位元列。<br>
#### 特性：
- 霍夫曼樹可用來編碼，也可用來解碼以達成資料壓縮的目的。
- 根據資料出現頻率多寡來建造的二元樹 。
- 霍夫曼樹的樹葉節點用以儲存資料元素 。
- 若該元素出現頻率愈高則從根節點到該元素所經過的節點路徑愈短，反之則愈長。
#### 結構：
step.1 從資料裡找出兩個出現頻率最低者，並將他們合併為新資料出現的頻率。<br>
step.2 將剛剛產生的新資料與下一個出現頻率最低者合併為新的資料，遞迴處理，直到所有節點都被放入霍夫曼樹之中。<br>
<img src="https://github.com/YuTe-Lai/yute-lai.github.io/blob/master/img/DS_Huffman_tree_structure.png?raw=true" alt="Huffman Tree"  width="600" height="300"><br>
step.3 樹被求出來之後，從根節點開始往左邊為'0'，往右為'1'（可以相反），將走到某一Leaf之前所經路程的值沃維資料的編碼。<br>
<img src="https://github.com/YuTe-Lai/yute-lai.github.io/blob/master/img/DS_Huffman_tree_structure2.png?raw=true" alt="Huffman Tree"  width="500" height="240"><br>
#### 資料壓縮率
- 原本的資料量：`8bit*(2+3+5+7+9+13) = 312`
- 霍夫曼編碼後：`2bit*(7+9+13) + 3bit*(3) + 4bit*(2+3) = 87`
- 壓縮率：`（1-(87/312)）*100% = 72.12%`

### 最大/最小堆積樹 Heaps Tree
堆積樹（Heap Tree）是一種完整二元樹，若堆積樹的父節點小於子節點，則稱之為最小堆積樹(Min Heap Tree)，若父節點大於子節點，則稱之為最大堆積樹(Max Heap Tree)。<br>
<img src="https://github.com/YuTe-Lai/yute-lai.github.io/blob/master/img/DS_Max_Heap_Tree.png?raw=true" alt="Max Heap Tree"  width="600" height="450">
#### 作法：
- 先將資料建立成完整二元樹。
- 在完整二元樹中找出最大值並依序移到樹根。
- 在完整二元樹中找出次大的值，並與其上一層的父節點比較，如果大於時，則交換，否則，不須作任何交換。
- 重覆步驟3，直到全部的節點的鍵值大於它的左子樹與右子樹的鍵值，即可成一棵最大堆積樹。
<br>
----------------------------------------------------------------------------------------------------------------------------
<img src="https://github.com/YuTe-Lai/yute-lai.github.io/blob/master/img/DS_Min_Heap_Tree.png?raw=true" alt="Min Heap Tree"  width="600" height="420">

#### 作法：
- 先將資料建立成完整二元樹。
- 在完整二元樹中找出最小值並依序移到樹根。
- 在完整二元樹中找出次小的值，並與其上一層的父節點比較，如果小於時，則交換，否則，不須作任何交換。
- 重覆步驟3，直到全部的節點的鍵值小於它的左子樹與右子樹的鍵值，即可成一棵最小堆積樹。


### 最大-最小堆積樹 Max-Min Heaps Tree
#### 定義：
最小-最大堆積樹(Min-Max Heaps Tree)是一個完整二元樹。此二元樹是交替的階層方式呈現，分別為最小階層 ( min level ) 和最大階層 ( max level ) ，其中樹根為最小鍵值。<br>
<img src="https://github.com/YuTe-Lai/yute-lai.github.io/blob/master/img/DS_Min_max_heaps_tree.png?raw=true" alt="Min-Max Heaps Tree"  width="611" height="300">

<img src="https://github.com/YuTe-Lai/yute-lai.github.io/blob/master/img/DS_Min_max_heaps_tree_rule.png?raw=true" alt="Min-Max Heaps Tree"  width="670" height="85">

### 雙向堆積樹 DEAPS
#### 定義
Deap是一個完整二元樹，它是可以為空，若不為空，則必須滿足下列特性：<br>
- 樹根不包含任何的元素。
- 左子樹為最小堆積樹(Min Heap)。
- 右子樹為最大堆積樹(Max Heap)。
- 左子樹節點鍵值必須要小於右子樹節點鍵值。
<img src="https://github.com/YuTe-Lai/yute-lai.github.io/blob/master/img/DS_DEAPS.png?raw=true" alt="DEAPS"  width="380" height="280">












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













