## Graphs

Definition:

- A graph is a collection of nodes (or vertices) and edges (connections between nodes).
- Graphs can be directed (edges have a direction) or undirected (edges do not have a direction).
- Graphs can be weighted (edges have weights) or unweighted (edges do not have weights).
- Graphs can be cyclic (contain cycles) or acyclic (do not contain cycles).
- Graphs can be connected (there is a path between every pair of nodes) or disconnected (some nodes are not reachable from others).

Degree of a Node:
- The degree of a node is the number of edges connected to it.
- In directed graphs, we distinguish between in-degree (number of incoming edges) and out-degree (number of outgoing edges).

Degree of Graph: 2 * Number of Edges

### Representation


```python
# adjacency list

from collections import defaultdict

adj = defaultdict(list)

def add_edge(u, v):
    adj[u].append(v)
    adj[v].append(u)  # for undirected graph, add both directions
```


```python
# adjacency matrix

mat = [[0] * 5 for _ in range(5)]
def add_edge_matrix(u, v):
    mat[u][v] = 1
    mat[v][u] = 1  # for undirected graph, set both directions
```

### Components of a Graph


```python
# number of components

from collections import defaultdict
def getComponents(V, edges):
    # create adj list
    adj= defaultdict(list)
    for e in edges:
        adj[e[0]].append(e[1])
        adj[e[1]].append(e[0])
    
    vis= [0] * V
    # dfs function to traverse a component
    def dfs(node, comp):
        if vis[node]:
            return
        
        vis[node]=1
        comp.append(node)
        
        for neighbor in adj[node]:
            dfs(neighbor, comp)
    
    # count the number of components
    ans= []
    count= 0
    for i in range(V):
        comp= []
        if vis[i]==0:
            dfs(i, comp)
            ans.append(comp)
            count+= 1
    return count, ans
```

### Traversal Algorithms


```python
# bfs

from collections import deque
def bfs(adj):
    ans= []
    vis= [0] * len(adj)
    q= deque([0])
    vis[0]= 1
    while q:
        node= q.popleft()
        ans.append(node)
        for neighbour in adj[node]:
            if vis[neighbour]==0:
                q.append(neighbour)
                vis[neighbour]=1
    return ans

# Time complexity of BFS is O(V + E) where V is the number of vertices and E is the number of edges.
# Space complexity is O(V) for the visited array and O(V) for the queue, leading to an overall space complexity of O(V)
```

Note: why can't we mark the node as visited when we append it to our ans instead of when we add it to the queue?

In BFS, you must mark a node as visited when you add it to the queue—not when you pop it from the queue or append it to the answer list. Here’s why:

If you mark a node as visited only when you pop it from the queue (or add to ans), the same node could be added to the queue multiple times by different neighbors. This wastes memory and time, and can even lead to incorrect results in some cases.
By marking it as visited when you enqueue it, you guarantee that each node is added to the queue at most once. This ensures correct BFS traversal and optimal performance.

Example: Suppose node 0 and node 1 are both connected to node 2. If you only mark node 2 as visited when you pop it, both 0 and 1 could enqueue 2, so 2 appears twice in the queue.


```python
# dfs

def dfs(adj):
    n= len(adj)
    vis= [0] * n
    ans= []
    def dfs(node):
        if vis[node]==1:
            return
        vis[node]= 1
        ans.append(node)
        for neighbour in adj[node]:
            dfs(neighbour)
    for node in range(n):
        dfs(node)
    return ans

# Time complexity of DFS is O(V + E) where V is the number of vertices and E is the number of edges.
# Space complexity is O(V) for the visited array and O(V) for the recursion stack, leading to an overall space complexity of O(V).
```


```python
# no of provinces

def findCircleNum(isConnected):
    ans, n= 0, len(isConnected)
    vis= [0] * n
    def dfs(node):
        if vis[node]==1:
            return
        vis[node]=1
        for i in range(n):
            if isConnected[node][i]==1:
                dfs(i)
    for node in range(n):
        if vis[node]==0:
            dfs(node)
            ans+=1
    return ans
```


```python
# rotten oranges

## tricky one - must revise!!

def orangesRotting(grid):
    countFresh= 0
    rottenOranges= []
    n, m= len(grid), len(grid[0])
    for i in range(n):
        for j in range(m):
            if grid[i][j]==1:
                countFresh+=1
            elif grid[i][j]==2:
                rottenOranges.append([i,j])
    if countFresh==0:
        return 0
    q= deque(rottenOranges)
    time= 0
    while q:
        size= len(q)
        if countFresh==0:
            return time
        for _ in range(size):
            cell= q.popleft()
            dir= [[0,-1], [0,1], [1,0], [-1,0]]
            for d in dir:
                x, y= cell[0]+d[0], cell[1]+d[1]
                if x>=0 and x<n and y>=0 and y<m and grid[x][y]==1:
                    q.append([x,y])
                    grid[x][y]= 2
                    countFresh-=1
        time+=1
    return -1
```


```python
# flood fill

def floodFill(image, sr, sc, color):
    n, m= len(image), len(image[0])
    def dfs(i, j):
        if image[i][j]==color:
            return
        oldCol= image[i][j]
        image[i][j]= color
        dir= [[-1,0], [1,0], [0,-1], [0,1]]
        for d in dir:
            x, y= i+d[0], j+d[1]
            if x>=0 and y>=0 and x<n and y<m and oldCol==image[x][y]:
                dfs(x, y)
    dfs(sr, sc)
    return image
```


```python
# check if cycle exists (using bfs)

def isCyclicBFS(adj):
    n= len(adj)
    vis= [0] * n
    q= deque()
    
    for i in range(n):
        if vis[i]==0:
            q.append((i, -1))
            vis[i]= 1
            
            while q:
                node, parent= q.popleft()
                
                for neighbour in adj[node]:
                    if vis[neighbour]==0:
                        vis[neighbour]= 1
                        q.append((neighbour, node))
                    elif neighbour!=parent:
                        return True 
    return False 

# check if cycle exists (using dfs)

def isCyclicDFS(adj):
    n= len(adj)
    vis= [0] * n
    def dfs(node, parent):
        vis[node]= 1
        for neighbour in adj[node]:
            if vis[neighbour]==0:
                if dfs(neighbour, node):
                    return True
            elif neighbour!=parent:
                return True
        return False
    for i in range(n):
        if vis[i]==0:
            if dfs(i, -1):
                return True
    return False
```


```python
# 0/1 matrix

def updateMatrix(mat):
    n, m= len(mat), len(mat[0])
    vis= [[0]*m for _ in range(n)]
    dist= [[0]*m for _ in range(n)]
    q= deque()
    for i in range(n):
        for j in range(m):
            if mat[i][j]==0:
                q.append([i, j, 0])
                vis[i][j]= 1
    while q:
        i, j, steps= q.popleft()
        dist[i][j]= steps
        direction= [[0,1], [0,-1], [-1,0], [1,0]]
        for d in direction:
            if i+d[0]>=0 and i+d[0]<n and j+d[1]>=0 and j+d[1]<m and vis[i+d[0]][j+d[1]]==0:
                q.append([i+d[0], j+d[1], steps+1])
                vis[i+d[0]][j+d[1]]= 1
    return dist          
```


```python
# surrounded regions

def solve(board):
    n, m= len(board), len(board[0])
    def dfs(i, j):
        if i<0 or j<0 or i==n or j==m or board[i][j]=="Y" or board[i][j]=="X":
            return

        board[i][j]="Y"
        dir= [[0,-1], [0,1], [1,0], [-1,0]]
        for d in dir:
            dfs(i+d[0], j+d[1])

    for i in [0,n-1]:
        for j in range(m):
            if board[i][j]=="O":
                dfs(i,j)

    for j in [0,m-1]:
        for i in range(n):
            if board[i][j]=="O":
                dfs(i,j)
    
    for i in range(n):
        for j in range(m):
            if board[i][j]=="Y":
                board[i][j]="O"
            else:
                board[i][j]="X"

    return
```


```python
# number of enclaves

def numEnclaves(grid):
    n, m= len(grid), len(grid[0])
    ans= 0
    def dfs(i, j):
        if i<0 or j<0 or i==n or j==m or grid[i][j]==0 or grid[i][j]==2:
            return
        
        grid[i][j]=2
        dir= [[0,-1], [0,1], [1,0], [-1,0]]
        for d in dir:
            dfs(i+d[0], j+d[1])

    for i in [0,n-1]:
        for j in range(m):
            if grid[i][j]==1:
                dfs(i,j)

    for j in [0, m-1]:
        for i in range(n):
            if grid[i][j]==1:
                dfs(i,j)

    for i in range(n):
        for j in range(m):
            if grid[i][j]==1:
                ans+=1
            elif grid[i][j]==2:
                grid[i][j]= 0
    return ans
```


```python
# word-ladder1

import string
def ladderLength(beginWord, endWord, wordList):
    wordMap= defaultdict(int)
    for word in wordList:
        wordMap[word]= 1
    wordMap[beginWord]= 0
    characters= list(string.ascii_lowercase)
    ans= 0
    q= deque([beginWord])
    while q:
        size= len(q)
        ans+= 1
        for i in range(size):
            word= q.popleft()
            for j in range(len(word)):
                for ch in characters:
                    if ch!= word[j]:
                        res = word[:j] + ch + word[j+1:]
                        if res==endWord and wordMap[res]:
                            return ans+1
                        if wordMap[res]>0:
                            q.append(res)
                            wordMap[res]= 0
    return 0
```


```python
# count distinct islands

def countDistinctIslands(grid):
    s, directions= set([]), [[0,-1], [0,1], [1,0], [-1,0]]
    n, m= len(grid), len(grid[0])
    def dfs(i, j, island, baseI, baseJ):
        if i<0 or j<0 or i==n or j==m or grid[i][j]==0:
            return
        
        island.append((i-baseI, j-baseJ))
        grid[i][j]=0
        
        for d in directions:
            dfs(i+d[0], j+d[1], island, baseI, baseJ)
    
    for i in range(n):
        for j in range(m):
            if grid[i][j]==1:
                island= []
                dfs(i, j, island, i, j)
                s.add(tuple(island))
    return len(s)
```

#### Bipartite Graphs

A graph that does not contains an odd length cycle is called a bipartite graph. So, if we start coloring the graph alternately no 2 adjacent nodes should have the same color, if it is a bipartite graph


```python
# check if a graph is bipartite

def isBipartite(graph):
    n= len(graph)
    color= [2] * n
    def dfs(node, col):
        color[node]= col
        for neighbour in graph[node]:
            if color[neighbour]==col:
                return False
            elif color[neighbour]==2:
                if not dfs(neighbour,1-col):
                    return False
        return True

    for node in range(n):
        if color[node]==2:
            if not dfs(node, 0):
                return False
    return True
```


```python
# longest cycle in a directed graph

def longestCycle(edges):
    n= len(edges)
    vis= [False] * n
    ans= -1
    for node in range(n):
        if vis[node]==False:
            curr= node
            path= {}
            step= 0
            while curr!=-1 and curr not in path and not vis[curr]:
                path[curr]= step
                vis[curr]= True
                step+= 1
                curr= edges[curr]
            if curr!=-1 and curr in path:
                ans= max(ans, step-path[curr])
    return ans
```
