# 演算法
演算法是一個有輸入跟輸出的解決問題的流程，它具有明確、有限步驟且有效的特性，常用於計算、資料處理和自動推理。通常在針對某一問題開發程式時，都會經過下列流程：<br>
## Step 1：明確定義問題
理論上來說，演算法可以解決大部分的問題，甚至要預測尚未發生的事情也並無不可能，但現實生活中的變數太多且難以量化，容易造成輸出結果不盡理想，故現階段在定義問題時建議可以先將問題簡單化。
<br>
## Step 2：設計演算法
### 演算法的定義：
高德納(Donald Ervin Knuth) 在《電腦程式設計藝術》裡歸納出一個演算法需要俱備的五個特性：<br>
1.輸入：一個演算法必須有0或多個輸入<br>
2.輸出：一個演算法應至少有一個或以上的輸出結果（ 有可能是 0 或是 null ）<br>
3.明確性：演算法的每個指令或步驟描述必須明確，以保證演算法的實際執行結果是確實符合要求<br>
4.有限性：在有限步驟後一定會結束，不會進入無窮迴圈<br>
5.有效性：又稱可行性。演算法中描述的步驟都是可以運算的<br>
<br>
而怎麼樣才能設計一個符合定義的演算法呢？常見的方法有兩種： **流程圖** 、 **虛擬碼** 。


<img src="https://github.com/YuTe-Lai/yute-lai.github.io/blob/master/img/flowchart.png?raw=true" alt="flowchart"  width="350" height="300">
<img src="https://github.com/YuTe-Lai/yute-lai.github.io/blob/master/img/virtualcode.png?raw=true" alt="virtualcode"  width="350" height="300"><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;流程圖&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;虛擬碼<br>
<br>
## Step 3：計算其執行時間及所使用的記憶體空間大小 

<br>
## Step 4：撰寫程式

<br>




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
## BinarySearchTree
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

