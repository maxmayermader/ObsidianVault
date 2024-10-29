###### Contents
1. [[#Array/List Operations]]
2. [[#Hash Table/Dictionary Template]] 
3. [[#Binary Search Template]]
4.  [[#Two Pointer Template]]
5.  [[#Sliding Window Template]]
6. [[#Stack Template]]
7. [[#Queue Template]]
9. [[#Tree Traversal Templates]]
10. [[#Graph Template (Adjacency List)]]
11. [[#Advanced Graphs]]
	- [[#Dijkstra's Algorithm]]
	- [[#Prim's Algorithm (MST)]]
	- [[#Bellman-Ford Algorithm]]
	- [[#Union Find Template]]
	- [[#Kruskal's Algorithm (MST)]]
	- [[#Topological Sort]]
13. [[#Heap/Priority Queue Template]]
14. [[#Backtracking Template]]
15. [[#Trie Template]]
16. [[#Intervals Template]]
17. [[#Greedy Template]]
18. [[#Dynamic Programming Templates]]
19. [[#Math & Geometry Template]]


## Array/List Operations 
[[Array and Hashing]]
**Keywords**: "sequence", "iteration", "in-place", "contiguous"
```python
# Basic array/list operations 
arr = []  # O(1) 
arr.append(x)  # O(1) amortized 
arr.pop()  # O(1) 
arr.insert(i, x)  # O(n) 
arr.remove(x)  # O(n) 
element = arr[i]  # O(1)
```


## Hash Table/Dictionary Template
[[Array and Hashing]]
**Keywords**: "frequency", "count", "unique", "pair"  
**Runtime**: O(1) average for most operations

```python
def hash_table_example():     
	hash_map = {}  # O(1)         
	
	# Insert    
	hash_map[key] = value  # O(1) average         
	
	# Lookup    
	if key in hash_map:  # O(1) average        
		value = hash_map[key]             
		
	# Delete    
	if key in hash_map:        
		del hash_map[key]  # O(1) average
```


## Binary Search Template
[[Binary Search]]
**Keywords**: "sorted", "search", "find", "rotated", "target"  
**Runtime**: O(log n)
```python
def binary_search(arr, target):     
	left, right = 0, len(arr) - 1         
	while left <= right:        
		mid = (left + right) // 2        
		if arr[mid] == target:            
			return mid        
		elif arr[mid] < target:            
			left = mid + 1        
		else:            
			right = mid - 1    
			
	return -1  # Not found`
```


## Two Pointer Template
[[Two Pointer]]
**Keywords**: "substring", "subarray", "palindrome", "reverse"  
**Runtime**: Usually O(n)

```python 
def two_pointer(arr):     
	left, right = 0, len(arr) - 1    
	result = 0         
	while left < right:        
	# Process elements from both ends        
	# Update pointers based on condition        
	if condition:            
		left += 1        
	else:            
		right -= 1    
	return result
```


## Sliding Window Template
[[Sliding Window]]
**Keywords**: "substring", "subarray", "consecutive", "at most k"  
**Runtime**: O(n)

```python
def sliding_window(arr):     
	left = curr = 0    
	result = 0         
	for right in range(len(arr)):        
		# Add arr[right] to window                 
		while window_condition_invalid:           
			# Remove arr[left] from window            
			left += 1                    
			
		# Update result             
	return result
```

## Linked List
[[Linked List]]
**Keywords**: Singly linked list, Node, Pointer, Sequential access
**Runtime**: Insertion: O(n) at the end, Search: O(n), Space Complexity: O(1) for operations

```python
class ListNode: 
	def __init__(self, val=0, next=None):
		self.val = val self.next = next 
		
class LinkedList: 
	def __init__(self): 
		self.head = None 
		
	def insert(self, val): 
		newNode = ListNode(val) 
		if not self.head: 
			self.head = newNode 
			return 
			
		current = self.head 
		while current.next: 
			current = current.next 
		current.next = newNode
```

### Fast and Slow Pointer Template
**Keywords**: Floyd's Cycle Detection, Tortoise and Hare, Two Pointers, Cycle Finding
**Runtime Complexity**:
- Time Complexity: O(n)
- Space Complexity: O(1)
- Cycle Detection: Guaranteed to find cycle in at most n step
```python
def floyd_cycle_detection(head): 
	if not head or not head.next: 
		return None 
		
	# Initialize pointers 
	slow = head 
	fast = head 
	
	# Find meeting point
	 while fast and fast.next: 
		 slow = slow.next 
		 fast = fast.next.next 
		 if slow == fast: 
			 return slow # Cycle detected 
	return None # No cycle found 
	
def find_cycle_start(head): 
	meeting_point = floyd_cycle_detection(head) 
	if not meeting_point: 
		return None 
		
	# Reset one pointer to head 
	pointer = head 
	while pointer != meeting_point: 
		pointer = pointer.next 
		meeting_point = meeting_point.next 
		
	return pointer # Start of cycle
```



## Stack Template
[[Stack]]
**Keywords**: "parentheses", "nested", "valid", "history"  
**Runtime**: O(n) for most operations

```python
class Stack:     
	def __init__(self):        
		self.stack = []  # O(1)             
		
	def push(self, x):  # O(1)        
		self.stack.append(x)             
	
	def pop(self):  # O(1)        
		if not self.is_empty():            
			return self.stack.pop()                 
			
	def peek(self):  # O(1)        
		if not self.is_empty():            
			return self.stack[-1]                 
			
	def is_empty(self):  # O(1)        
		return len(self.stack) == 0
```



## Queue Template
**Keywords**: "first", "order", "level", "BFS"  
**Runtime**: O(1) for most operations

```python
from collections import deque class Queue:     
	def __init__(self):        
		self.queue = deque()  # O(1)             
		
	def enqueue(self, x):  # O(1)        
		self.queue.append(x)             
		
	def dequeue(self):  # O(1)        
		if not self.is_empty():            
			return self.queue.popleft()                 
			
	def front(self):  # O(1)        
		if not self.is_empty():            
			return self.queue[0]                 
			
	def is_empty(self):  # O(1)        
		return len(self.queue) == 0`
```



## Tree Traversal Templates
[[Trees]]
**Keywords**: "binary tree", "depth", "path", "root"  
**Runtime**: O(n) for full traversal

```python
class TreeNode:     
	def __init__(self, val=0):        
		self.val = val        
		self.left = None        
		self.right = None 
		
# DFS - Inorder 
def inorder(root):     
	if not root:        
		return    
	inorder(root.left)    
	print(root.val)    
	inorder(root.right) 
	
# BFS - Level Order 
def level_order(root):     
	if not root:        
		return []    
	queue = deque([root])    
	result = []         
	while queue:        
		level = []        
		for _ in range(len(queue)):            
			node = queue.popleft()            
			level.append(node.val)            
			if node.left:                
				queue.append(node.left)            
			if node.right:                
				queue.append(node.right)        
		result.append(level)    
	return result
```



## Graph Template (Adjacency List)
[[Graphs]]
**Keywords**: "connected", "path", "cycle", "neighbors"  
**Runtime**: O(V + E) for full traversal

```python
from collections import defaultdict 

class Graph:     
	def __init__(self):        
		self.graph = defaultdict(list)             
		
	def add_edge(self, u, v):        
		self.graph[u].append(v)             
		
	def bfs(self, start):        
		visited = set()        
		queue = deque([start])        
		visited.add(start)                 
		while queue:            
			vertex = queue.popleft()            
			for neighbor in self.graph[vertex]:                
				if neighbor not in visited:    
					visited.add(neighbor)        
					queue.append(neighbor)                         
					
	def dfs(self, vertex, visited=None):        
		if visited is None:            
			visited = set()        
		visited.add(vertex)                 
		for neighbor in self.graph[vertex]:            
			if neighbor not in visited:                
				self.dfs(neighbor, visited)
```



## Advanced Graphs
[[Advanced Graphs]]
### Dijkstra's Algorithm
**Keywords**: "shortest path", "weighted", "non-negative edges"  
**Runtime**: O(E log V) with priority queue

```python
def dijkstra(graph, start):     
	distances = {node: float('inf') for node in graph}    
	distances[start] = 0    
	pq = [(0, start)]    
	visited = set()         
	
	while pq:        
		curr_dist, curr = heapq.heappop(pq)                 
		if curr in visited:            
			continue                     
		visited.add(curr)                 
		for neighbor, weight in graph[curr].items():            
			distance = curr_dist + weight                         
				if distance < distances[neighbor]:                
					distances[neighbor] = distance                
					heapq.heappush(pq, (distance, neighbor))                     
	return distances

def dijkstra(self, grid: List[List[int]]) -> int: 
	ROWS, COLS = len(grid), len(grid[0]) # Grid dimensions 
	# Initialize visited set and priority queue 
	visited = set() 
	minHeap = [[0, 0, 0]] # [distance/cost/time, row, col] 
	
	# Possible directions (can be modified based on problem) 
	directions = [[0, 1], [0, -1], [1, 0], [-1, 0]] # For diagonal movement add: [1,1], [1,-1], [-1,1], [-1,-1] 
	
	# Add starting position to visited 
	visited.add((0, 0)) 
	while minHeap: 
		dist, row, col = heapq.heappop(minHeap) # Get current position with minimum distance 
		# Check if reached destination (modify based on problem) 
		if row == ROWS - 1 and col == COLS - 1: 
			return dist 
			
		# Explore neighbors 
		for dx, dy in directions: 
			newRow, newCol = row + dx, col + dy 
			# Check boundaries and visited state 
			if (newRow < 0 or newCol < 0 
			or newRow >= ROWS or newCol >= COLS
			or (newRow, newCol) in visited): 
				continue 
				# Mark as visited 
				visited.add((newRow, newCol)) 
				# Calculate new distance (modify based on problem) 
				newDist = max(dist, grid[newRow][newCol]) # Example calculation 
				# Alternative calculations: 
				# newDist = dist + grid[newRow][newCol] 
				# For cumulative path 
				# newDist = max(dist, abs(grid[newRow][newCol] - grid[row][col])) for difference 
				
				# Add to priority queue 
				heapq.heappush(minHeap, [newDist, newRow, newCol]) 
			
	return -1 # If no path found
```

### Prim's Algorithm (MST)
**Keywords**: "minimum spanning tree", "connected", "undirected"  
**Runtime**: O(E log V) with priority queue

```python
def prims(graph):     
	start_vertex = list(graph.keys())[0]    
	mst = set()    
	visited = {start_vertex}    
	edges = [(cost, start_vertex, to) for to, cost in
			graph[start_vertex].items()]    
	heapq.heapify(edges)         
	
	while edges:        
		cost, frm, to = heapq.heappop(edges)                 
		if to not in visited:           
			visited.add(to)            
			mst.add((frm, to, cost))                         
			for next_to, next_cost in graph[to].items():                
				if next_to not in visited:                    
					heapq.heappush(edges, (next_cost, to, next_to))                       
	return mst
```

### Bellman-Ford Algorithm
**Keywords**: "negative edges", "negative cycles", "shortest path"  
**Runtime**: O(VE)

```python
def bellman_ford(graph, start):     
	distances = {node: float('inf') for node in graph}    
	distances[start] = 0         
	# Relax all edges V-1 times    
	for _ in range(len(graph) - 1):        
		for u in graph:            
			for v, weight in graph[u].items():                
				if distances[u] + weight < distances[v]:                    
					distances[v] = distances[u] + weight        
					
	# Check for negative cycles    
	for u in graph:        
		for v, weight in graph[u].items():            
			if distances[u] + weight < distances[v]:                
				return None  # Negative cycle exists                     
				
	return distances
```

### Union Find Template
**Keywords**: "connected components", "groups", "islands", "connections"  
**Runtime**: O(α(n)) ≈ O(1) for union and find operations

```python
class UnionFind:     
	def __init__(self, n):        
		self.parent = list(range(n))        
		self.rank = [0] * n         
		
	def find(self, x):        
		if self.parent[x] != x:            
			self.parent[x] = self.find(self.parent[x])  # Path compression 
		return self.parent[x]         
		
	def union(self, x, y):        
		px, py = self.find(x), self.find(y)        
		if px == py:            
			return False                 
			
		# Union by rank        
		if self.rank[px] < self.rank[py]:            
			px, py = py, px        
		self.parent[py] = px        
		if self.rank[px] == self.rank[py]:            
			self.rank[px] += 1        
		return True
```

### Kruskal's Algorithm (MST)
**Keywords**: "minimum spanning tree", "disjoint set", "union find"  
**Runtime**: O(E log E)

```python
def kruskals(graph):     
	edges = []    
	for u in graph:        
		for v, weight in graph[u].items():            
			edges.append((weight, u, v))         
		edges.sort()  # Sort by weight    
		uf = UnionFind(graph.keys())    
		mst = []         
		for weight, u, v in edges:        
			if uf.union(u, v):            
				mst.append((u, v, weight))                 
				
	return mst
```

### Topological Sort
**Keywords**: "dependencies", "DAG", "ordering", "prerequisites"  
**Runtime**: O(V + E)

```python
def topological_sort(graph):     
	indegree = {node: 0 for node in graph}    
	for node in graph:        
		for neighbor in graph[node]:            
			indegree[neighbor] += 1         
	queue = deque([node for node, count in indegree.items() if count == 0])   
	result = []         
	
	while queue:        
		node = queue.popleft()        
		result.append(node)                 
		for neighbor in graph[node]:            
			indegree[neighbor] -= 1            
			if indegree[neighbor] == 0:                
				queue.append(neighbor)                     
				
	return result if len(result) == len(graph) else []  # Check for cycles
```



## Heap/Priority Queue Template
[[Heap/PQ]]
**Keywords**: "k largest", "k smallest", "median"  
**Runtime**: O(log n) for push/pop operations

```python
import heapq 

class PriorityQueue:     
	def __init__(self):        
		self.heap = []    
		         
	def push(self, x):  # O(log n)        
		heapq.heappush(self.heap, x)             
	
	def pop(self):  # O(log n)        
		if not self.is_empty():            
		return heapq.heappop(self.heap)                 
		
	def peek(self):  # O(1)        
		if not self.is_empty():            
			return self.heap[0]                 
			
	def is_empty(self):  # O(1)        
		return len(self.heap) == 0`
```



## Backtracking Template
[[Backtracking]]
**Keywords**: "combinations", "permutations", "subsets", "generate"  
**Runtime**: Usually O(2 $^{n}$) or O(n!)

```python
def backtrack(arr, curr_path, result):     \
	# Base case - add solution    
	if is_valid_solution(curr_path):        
		result.append(curr_path[:])        
		return             
		
	for i in range(len(arr)):        
		# Skip invalid choices        
		if not is_valid_choice(arr[i]):            
			continue                     
			
		# Make choice        
		curr_path.append(arr[i])                 
		
		# Recurse        
		backtrack(arr, curr_path, result)                 
		
		# Undo choice        
		curr_path.pop()`
```



## Trie Template
[[Tries]]
**Keywords**: "prefix", "word search", "dictionary", "autocomplete"  
**Runtime**: O(n) for insertion/search where n is word length

```python
class TrieNode:     
	def __init__(self):        
		self.children = {}        
		self.is_end = False 
		
class Trie:     
	def __init__(self):        
		self.root = TrieNode()         
		
	def insert(self, word):  # O(n)        
		curr = self.root        
		for char in word:            
			if char not in curr.children:                
				curr.children[char] = TrieNode()            
			curr = curr.children[char]        
		curr.is_end = True         
		
	def search(self, word):  # O(n)        
		curr = self.root        
		for char in word:            
			if char not in curr.children:                
				return False            
			curr = curr.children[char]        
		return curr.is_end         
		
	def starts_with(self, prefix):  # O(n)        
		curr = self.root        
		for char in prefix:           
			if char not in curr.children:                
				return False            
			curr = curr.children[char]        
		return True
```


## Intervals Template\
[[Intervals]]
**Keywords**: "meeting rooms", "merge", "overlap", "schedule"  
**Runtime**: O(n log n) due to sorting

```python
def interval_template(intervals):     
	# Sort intervals by start time    
	intervals.sort(key=lambda x: x[0])         
	result = []    
	curr_interval = intervals[0]         
	for interval in intervals[1:]:        
	# Check for overlap        
	if curr_interval[1] >= interval[0]:            
		# Merge intervals            
		curr_interval[1] = max(curr_interval[1], interval[1])        
	else:            
		# Add non-overlapping interval 
		result.append(curr_interval[:])            
		curr_interval = interval         
	
	result.append(curr_interval)    
	return result
```



## Greedy Template
[[Greedy]]
**Keywords**: "maximum", "minimum", "optimal", "earliest", "latest"  
**Runtime**: Usually O(n) or O(n log n)

```python
def greedy_template(arr):     
	# Sort if needed   
	arr.sort()  # O(n log n)         
	result = 0    
	curr = 0         
	for num in arr:        
		# Make locally optimal choice        
		if is_valid_choice(num):            
			curr += num            
			result = max(result, curr)        
		else:            
			curr = 0         
	return result
```



## Dynamic Programming Templates
[[1 DP]]
**Keywords**: "maximum", "minimum", "optimal", "ways", "count"
##### **1D Dynamic Programming**  
**Runtime**: O(n) typically

```python
def dp_1d(arr):     
	n = len(arr)    
	dp = [0] * (n + 1)  # Initialize dp array         
	
	# Base cases    
	dp[0] = base_value         
	
	# Fill dp array    
	for i in range(1, n + 1):        
		dp[i] = max(dp[i-1] + arr[i], arr[i])  
		
	# Example recurrence         
	return max(dp)  # or dp[-1] depending on problem`
```

[[]]
##### **2D Dynamic Programming**  
**Runtime**: O(m$*$n) typically

```python
def dp_2d(grid):     
	m, n = len(grid), len(grid[0])    
	dp = [[0] * (n + 1) for _ in range(m + 1)]         
	
	# Base cases    
	dp[0][0] = base_value         
	
	# Fill dp array    
	for i in range(1, m + 1):        
		for j in range(1, n + 1):            
			dp[i][j] = min(dp[i-1][j], dp[i][j-1]) + grid[i-1][j-1]
	return dp[m][n]`
```



## Math & Geometry Template
[[]]
**Keywords**: "matrix", "rotate", "spiral", "diagonal"  
**Runtime**: Varies by problem

```python
def matrix_operations(matrix):     
	n = len(matrix)         
	# Rotate matrix 90 degrees clockwise    
	
	def rotate():        
		for i in range(n // 2):            
			for j in range(i, n - i - 1):                
				temp = matrix[i][j]                
				matrix[i][j] = matrix[n-1-j][i]                
				matrix[n-1-j][i] = matrix[n-1-i][n-1-j]                
				matrix[n-1-i][n-1-j] = matrix[j][n-1-i]                
				matrix[j][n-1-i] = temp         
				
	# Transpose matrix    
	def transpose():        
		for i in range(n):            
			for j in range(i, n):                
				matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]         
				
	# Reflect matrix horizontally    
	def reflect():        
		for i in range(n):            
			for j in range(n // 2):                
				matrix[i][j], matrix[i][n-1-j] = matrix[i][n-1-j], matrix[i][j]
```
