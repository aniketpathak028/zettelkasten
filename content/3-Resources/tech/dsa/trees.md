## Trees

Basic Terms:-

1. Root - topmost node in a tree
2. Children - every node except root is a child to another node
3. Leaf node - a node that does not have any children
4. Sub tree - each node can be considered as a root node for a subtree


Types of Trees:-

1. Full binary trees - 0 or 2 children
2. Complete binary tree - all levels are fully filled except the last level, which is filled from left to right
3. Perfect binary tree - all internal nodes have exactly two children, and all leaf nodes are at the same level
4. Balanced binary tree -  the height difference between left and right subtrees of any node is at most 1
5. Degenerate tree -  each parent node has only one child ie. skew tree or linked list


```python
# Representation

class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
```


```python
# Inorder Traversal (Left, Root, Right)

def inorder(root):
    if root == None:
        return []
    return inorder(root.left) + [root.val] + inorder(root.right)

# Preorder Traversal (Root, Left, Right)

def preorder(root):
    if root == None:
        return []
    return [root.val] + preorder(root.left) + preorder(root.right)

# Postorder Traversal (Left, Right, Root)

def postorder(root):
    if root == None:
        return []
    return postorder(root.left) + postorder(root.right) + [root.val]

# Time complexity: O(n) because we visit each node exactly once
# Space complexity: O(n) because of the recursion stack
```


```python
# Level order traversal

from collections import deque

def levelorder(root):
        if not root:
            return []

        ans= []
        queue= deque([root])

        while queue:
            level= []
            for _ in range(len(queue)):
                node= queue.popleft()
                level.append(node.val)
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
            ans.append(level)

        return ans

# T.C = O(n) because we visit each node exactly once
# S.C = O(n) because of the queue
```


```python
# iterative perorder traversal (alternative)

def preorder_iterative(root):
    if not root:
        return []

    stack= [root]
    ans= []

    while stack:
        node= stack.pop()
        ans.append(node.val)
        if node.right:
            stack.append(node.right)
        if node.left:
            stack.append(node.left)

    return ans

# iterative inorder traversal (alternative)

def inorder_iterative(root):
    if not root:
        return []

    stack= []
    ans= []
    node= root

    while stack or node:
        while node:
            stack.append(node)
            node= node.left
        node= stack.pop()
        ans.append(node.val)
        node= node.right
    
    return ans

# iterative postorder traversal (alternative)

def postorder_iterative(root):
    if not root:
        return []

    stack= [root]
    ans= []

    while stack:
        node= stack.pop()
        ans.append(node.val)
        if node.left:
            stack.append(node.left)
        if node.right:
            stack.append(node.right)

    return ans[::-1]
```


```python
# height of a binary tree

def height(root):
    if not root:
        return 0
    
    return 1 + max(height(root.left), height(root.right))
```


```python
# diameter of a binary tree

def solve(root):
    if root==None:
        return 0

    left= solve(root.left)
    right= solve(root.right)

    maxi= max(maxi, left+right)

    return 1 + max(left, right)
```


```python
# max path sum

def solve(root):
    if root==None:
        return 0

    left= solve(root.left)
    right= solve(root.right)

    maxi= max(maxi, max(root.val, max(root.val+left, max(root.val+right, root.val+right+left))))

    return max(left+root.val, max(right+root.val, root.val))
```


```python
# check if 2 trees are identical

def isSameTree(p, q):
    if p==None and q==None:
        return True
    elif p==None or q==None:
        return False
    else:
        if p.val!=q.val:
            return False
        else:
            return isSameTree(p.left, q.left) and isSameTree(p.right, q.right)
```


```python
# zig-zag traversal

def zigzagLevelOrder(root):
    q= deque()
    q.append(root)
    flag= True # reverse level when false
    ans= []
    if root==None:
        return ans
    while len(q)>0:
        size= len(q)
        level= []
        while size>0:
            size-=1
            node= q.popleft()
            level.append(node.val)
            if node.left:
                q.append(node.left)
            if node.right:
                q.append(node.right)
        if flag:
            ans.append(level[:])
            flag= False
        else:
            ans.append(level[::-1])
            flag= True
    return ans
```


```python
# vertical order traversal

# dic: {
#     -1:{
#         1: [9]
#     },
#     0:{
#         0: [3]
#         2: [15]
#     },
#     1:{
#         1: [20]
#     },
#     2:{
#         2: [7]
#     }
# }

from collections import defaultdict
def solve(root, i, j, dic):
    if root is None:
        return
    
    dic[j][i].append(root.val)
    solve(root.left, i + 1, j - 1, dic)
    solve(root.right, i + 1, j + 1, dic)

def verticalTraversal(root):
    dic = defaultdict(lambda: defaultdict(list))
    solve(root, 0, 0, dic)

    ans = []
    for j in sorted(dic.keys()):
        column = []
        for i in sorted(dic[j].keys()):
            column += sorted(dic[j][i])
        ans.append(column)

    return ans
```


```python
# top view of tree

from collections import defaultdict

def solve(root, i, j, dic):
    if root==None:
        return
    
    dic[j][i].append(root.data)
    solve(root.left, i+1, j-1, dic)
    solve(root.right, i+1, j+1, dic)
        
def topView(root):
    dic= defaultdict(lambda: defaultdict(list))
    solve(root, 0, 0, dic)
    ans= []
    for i in sorted(dic.keys()):
        for j in sorted(dic[i].keys()):
            ans.append(dic[i][j][0])
            break
    return ans
```


```python
# bottom view of tree

def solve(root, i, j, dic):
    if root==None:
        return
    
    dic[j][i].append(root.data)
    solve(root.left, i+1, j-1, dic)
    solve(root.right, i+1, j+1, dic)
        
def bottomView(root):
    dic= defaultdict(lambda: defaultdict(list))
    solve(root, 0, 0, dic)
    
    ans= []
    for j in sorted(dic.keys()):
        max_key= max(dic[j].keys())
        ans.append(dic[j][max_key][-1])
            
    return ans
```


```python
# right side view

def rightSideView(root):
    ans= []
    if root==None:
        return ans
    q= deque()
    q.append(root)
    while len(q)>0:
        size= len(q)
        last= -1
        while size>0:
            size-= 1
            node= q.popleft()
            last= node.val
            if node.left:
                q.append(node.left)
            if node.right:
                q.append(node.right)
        ans.append(last)
    return ans
```


```python
# check if tree is symmetric or not

def check(p, q):
    if p==None and q==None:
        return True
    elif p==None or q==None:
        return False

    if p.val==q.val:
        return check(p.left, q.right) and check(p.right, q.left)
    else:
        return False

def isSymmetric(root):
    if root==None:
        return True
    else:
        return check(root.left, root.right)
```


```python
# root to node path

def findPath(root, num, path):
    if root==None:
        return False
    
    if root.val==num:
        path.append(root.val)
        return True
        
    path.append(root.val)
    if findPath(root.left, num, path) or findPath(root.right, num, path):
        return True
    else:
        path.pop()
        return False
            
def solve(root, num):
    path= []
    findPath(root, num, path)
    return path
```


```python
# find lca

lca = None
def solve(root, p, q):
    if root==None:
        return False

    if root==p or root==q:
        lca= root
        return True

    left= solve(root.left, p, q)
    right= solve(root.right, p, q)

    if left and right:
        lca= root
        return True
    elif left or right:
        return True
    else:
        return False
```


```python
# width of binary tree

def widthOfBinaryTree(root):
    if root==None:
        return 0
    q= deque([(root, 1)])
    maxWidth= -1
    while q:
        size= len(q)
        _, first_index= q[0]
        last_index= -1
        for _ in range(size):
            node, last_index= q.popleft()
            if node.left:
                q.append((node.left, last_index*2))
            if node.right:
                q.append((node.right, last_index*2+1))
        width= last_index-first_index+1 if size>1 else 1
        maxWidth=max(maxWidth, width)
    return maxWidth
```


```python
# children sum

def isSumProperty(root):
    if root==None or (root.left==None and root.right==None):
        return 1
        
    left= root.left.data if root.left else 0
    right= root.right.data if root.right else 0
    
    if left+right==root.data:
        return isSumProperty(root.left) * isSumProperty(root.right)
    else:
        return 0
```


```python
# count complete tree nodes

def exists(root, index, s, e):
        if root==None:
            return False

        if s==e:
            return True

        half= (s+e)//2
        if index <= half:
            return exists(root.left, index, s, half)
        else:
            return exists(root.right, index, half+1, e)
        

def countNodes(self, root) -> int:
    if not root:
        return 0

    # height of the tree
    h, temp= 0, root
    while temp.left:
        temp = temp.left
        h += 1
    
    # last row contains nodes [0->2*h-1]
    # do a bs on mid and find out the leftmost node
    low, high= 0, 2**h - 1
    while low<=high:
        mid= low + (high-low)//2
        if self.exists(root, mid, 0, 2**h - 1):
            low= mid+1
        else:
            high= mid-1
    return 2**h + low - 1
```


```python
# burning tree - more like a graph problem

def convert(root, adj):
    if root==None:
        return 
    
    if root.left:
        adj[root.data].append(root.left.data)
        adj[root.left.data].append(root.data)
        
    if root.right:
        adj[root.data].append(root.right.data)
        adj[root.right.data].append(root.data)
        
    convert(root.left, adj)
    convert(root.right, adj)
        
def minTime(root, target):
    # convert the tree into graph
    adj= defaultdict(list)
    convert(root, adj)
    
    # do a bfs from target and keep a timer that increments for each level
    max_node = max(adj.keys()) if adj else target
    vis= [0] * (max_node+1)
    q= deque([target])
    vis[target]= 1
    time= 0
    while q:
        for _ in range(len(q)):
            node= q.popleft()
            for neighbour in adj[node]:
                if not vis[neighbour]:
                    q.append(neighbour)
                    vis[neighbour]= 1
                    
        if q:
            time+= 1
    # return timer once bfs is completed
    return time
```

#### convert a tree into graph

- create an adjacent list
```
    adj= defaultdict(list)

    dfs(root, adj) # for each node add its children and parent as neighbours
```

### construct a unique binary tree using traversals

- Inorder(root->left->right) and Preorder(root->left->right): can construct a unique binary tree
- Inorder(root->left->right) and Postorder(root->left->right): can construct a unique binary tree
- Preorder(root->left->right) and Postorder(root->left->right): cannot construct a unique binary tree because we cannot determine the left and right subtrees
   


```python
# construct binary tree from inorder and preorder

def solve(root, preorder, preStart, preEnd, inorder, inStart, inEnd, map):
        if inStart>inEnd:
            return None

        rootEle= preorder[preStart]
        root= TreeNode(rootEle)
        noLeft, noRight= map[rootEle]-inStart, inEnd-map[rootEle]
        root.left= solve(root.left, preorder, preStart+1, preStart+noLeft, inorder, inStart, map[rootEle]-1, map)
        root.right= solve(root.right, preorder, preStart+noLeft+1, preEnd, inorder, map[rootEle]+1, inEnd, map)
        return root

def buildTree(preorder, inorder):
    map= {val: idx for idx,val in enumerate(inorder)}
    return solve(None, preorder, 0, len(preorder)-1, inorder, 0, len(inorder)-1, map)

# Time complexity: O(n)
# Space complexity: O(n) for the map
# and O(n) for the recursion stack
```


```python
# construct binary tree from inorder and postorder

def solve(root, inorder, inStart, inEnd, postorder, postStart, postEnd, map):
        if inStart>inEnd:
            return None

        rootEle, idxInorder= postorder[postEnd], map[postorder[postEnd]]
        root= TreeNode(rootEle)
        eleLeft= idxInorder - inStart
        eleRight= inEnd - idxInorder

        root.right= solve(root.right, inorder, idxInorder+1, inEnd, postorder, postEnd-eleRight, postEnd-1, map)
        root.left= solve(root.left, inorder, inStart, idxInorder-1, postorder, postStart, postStart+eleLeft-1, map)
        return root
        
def buildTree(postorder, inorder):
    map= {val: idx for idx,val in enumerate(inorder)}
    return solve(None, inorder, 0, len(inorder)-1, postorder, 0, len(postorder)-1, map)

# Time complexity: O(n)
# Space complexity: O(n)
```


```python
# serialize and deserialize binary tree

def serialize(root):
    if root==None:
        return "N"
    
    return str(root.val) + "," + serialize(root.left) + "," + serialize(root.right)

def deserialize(data):
    values = data.split(",")
    return deserialize_helper(values)

def deserialize_helper(values):
    if not values:
        return None
    value = values.pop(0)
    if value == "N":
        return None
    root = TreeNode(int(value))
    root.left = deserialize_helper(values)
    root.right = deserialize_helper(values)
    return root

# Time complexity: O(n)
# Space complexity: O(n) for the stack
```

## Binary Search Trees


```python
# search in a bst

def searchBST(root, val):
    if root==None:
        return None
    
    if root.val==val:
        return root

    if val<root.val:
        return searchBST(root.left, val)
    else:
        return searchBST(root.right, val)
```


```python
# find min/max in a bst

def findMin(root):
    if root==None:
        return None
    
    while root.left:
        root= root.left
    return root

def findMax(root):
    if root==None:
        return None
    
    while root.right:
        root= root.right
    return root
```


```python
# find ceil in a bst

def findCeil(root, inp):
    ans= -1
    while root:
        if root.key==inp:
            return inp
        elif root.key<inp:
            root= root.right
        else:
            ans= root.key
            root= root.left
    return ans
```


```python
# find floor in a bst

def floor(root, x):
    ans= -1
    while root:
        if root.data==x:
            return x
        elif root.data>x:
            root= root.left
        else:
            ans= root.data
            root= root.right
    return ans
```


```python
# insert into a bst

def insertIntoBST(root, val):
    if not root:
        return TreeNode(val)
    rootCpy= root
    while rootCpy:
        if rootCpy.val<val:
            if rootCpy.right:
                rootCpy= rootCpy.right
            else:
                rootCpy.right= TreeNode(val)
                return root
        elif rootCpy.val>val:
            if rootCpy.left:
                rootCpy= rootCpy.left
            else:
                rootCpy.left= TreeNode(val)
                return root
    return root
```


```python
# delete a node in a bst

def deleteNode(root, key):
    rootCpy= root
    while root:
        if root.val==key:
            return delete(root)
        elif root.left and root.left.val==key:
            root.left= delete(root.left)
            break
        elif root.right and root.right.val==key:
            root.right= delete(root.right)
            break
        else:
            if root.val>key:
                root= root.left
            else:
                root= root.right
    return rootCpy
def delete(root):
    # find the rightmost node in the left subtree
    if root.left==None:
        return root.right
    rightMostNode= root.left
    while rightMostNode.right:
        rightMostNode= rightMostNode.right
    # attach the right subtree in the left most node of the left subtree
    rightMostNode.right= root.right
    return root.left
```


```python
# kth smallest element in a bst

def inorder(root, arr, k):
    if root==None:
        return

    if len(arr)==k:
        return

    inorder(root.left, arr, k)
    arr.append(root.val)
    inorder(root.right, arr, k)

def kthSmallest(root, k):
    arr= []
    inorder(root, arr, k)
    return arr[k-1]
```


```python
# validate bst

def isValidBST(root):
    def solve(root, low, high):
        if root==None:
            return True

        if root.val<=low or root.val>=high:
            return False

        return solve(root.left, low, root.val) and solve(root.right, root.val, high)

    return solve(root, float("-inf"), float("inf"))
# Time complexity: O(n)
# Space complexity: O(h) for the recursion stack
```


```python
# lca of a bst

def lowestCommonAncestor(root, p, q):
    if root==None:
        return None

    if root.val>p.val and root.val>q.val:
        return lowestCommonAncestor(root.left, p, q)
    elif root.val<p.val and root.val<q.val:
        return lowestCommonAncestor(root.right, p, q)
    else:
        return root
```


```python
# construct bst from preorder

def build(pre, arr, root, bound):
    index= arr[0]
    if index==len(pre) or pre[index]>bound:
        return None

    if pre[index]<bound:
        root= TreeNode(pre[index])
        arr[0]+= 1
        root.left= build(pre, arr, root.left, root.val)
        root.right= build(pre, arr, root.right, bound)
        return root
    else:
        return None

def bstFromPreorder(preorder):
    arr= [0]
    return build(preorder, arr, None, sys.maxsize)
```


```python
# 2 sum for bst

def findTarget(root, k):
    # take an inorder and maintain a hashmap
    stack, inorder= [], []
    m, node= {}, root
    while node or stack:
        while node:
            stack.append(node)
            node= node.left
        node= stack.pop()
        inorder.append(node.val)
        if node.val in m:
            m[node.val]+=1
        else:
            m[node.val]= 1
        node= node.right
    # traverse the list and check if a couple exists
    for ele in inorder:
        if k-ele==ele:
            return True if m[ele]>1 else False
        if k-ele in m:
            return True

    return False
```


```python
# recover bst

import sys
def inorder(self, root):
    if root==None:
        return

    self.inorder(root.left)
    if root.val<self.prev.val:
        if self.first:
            self.last= root
            return
        else:
            self.first= self.prev
            self.mid= root
    self.prev= root
    self.inorder(root.right)

def recoverTree(self, root):
    self.last, self.mid, self.first= None, None, None
    self.prev= TreeNode(-sys.maxsize-1)
    self.inorder(root)
    if self.last:
        self.first.val, self.last.val= self.last.val, self.first.val
    else:
        self.first.val, self.mid.val= self.mid.val, self.first.val
```


```python
# BST iterator

class BSTIterator:
    def __init__(self, root):
        self.stack= []
        temp= root
        while temp:
            self.stack.append(temp)
            temp= temp.left

    def next(self) -> int:
        top= self.stack.pop()
        if top.right:
            temp= top.right
            while temp:
                self.stack.append(temp)
                temp= temp.left
        return top.val

    def hasNext(self) -> bool:
        return True if len(self.stack)>0 else False
```


```python
# largest bst in a binary tree

def largestBst(self, root):
    def helper(node):
        if node is None:
            return 0, float('inf'), float('-inf')
        
        lSize, lMin, lMax = helper(node.left)
        rSize, rMin, rMax = helper(node.right)
        
        if lMax < node.data < rMin:
            size = 1 + lSize + rSize
            return size, min(lMin, node.data), max(rMax, node.data)
        else:
            return max(lSize, rSize), float('-inf'), float('inf')

    ans, _, _ = helper(root)
    return ans
```
