#### [[Templates]]

## [787. Cheapest Flights Within K Stops](https://leetcode.com/problems/cheapest-flights-within-k-stops/)
### Steps
- ***Bellman ford algo***
- cost array with node set to cost
- Set all costs to infinity except src which is 0
- stops = k+1
- bfs through layers
	- copy cost array
	- go through all nodes
		- if  cost is inf then skip
		- if src cost and cost to new node is less than dest node cost then set new temp cost
	- set copy to cost array
- return dest cost 
	- if inf then -1

#### Code
```python

```

## [269. Alien Dictionary](https://leetcode.com/problems/alien-dictionary/)
### Steps
- chars of a word not in order, the words are in order, find adjacency list of each unique char by iterating through adjacent words and finding first chars that are different, run topsort on graph and do loop detection;

#### Code
```python
class Solution:
    def alienOrder(self, words: List[str]) -> str:
        adj = {c:set() for w in words for c in w}
        for i in range(len(words)-1):
            w1, w2 = words[i], words[i+1]
            minLen = min(len(w2), len(w1))
            if len(w1) > len(w2) and w1[:minLen] == w2[:minLen]:
                return ''

            for j in range(minLen):
                if w1[j] != w2[j]:
                    adj[w1[j]].add(w2[j])
                    break

        visit = {}
        res = []
        print(adj)

        def dfs(c):
            if c in visit:
                return visit[c]

            visit[c] = True

            for nei in adj[c]:
                if dfs(nei):
                    return True

            visit[c] = False
            res.append(c)

        for c in adj:
            if dfs(c):
                return ''
        res.reverse()
        return "".join(res)

```


## [332. Reconstruct Itinerary](https://leetcode.com/problems/reconstruct-itinerary/)
### Steps
- adj list 
- sort adj values
- dfs until no more neigbours
	- remove visited neihbours from adacny list
	- keep visiting until no more neighbours
	- once done append src to res
- reverse list
- return if len(res) is the same as len(tickets) + 1
	- You start at which is not included in tickets included (home -> JFK)
- else return []

#### Code
```python
class Solution:
    def findItinerary(self, tickets: List[List[str]]) -> List[str]:
        adj = {src:[] for src, dst in tickets}
        for src, dst in tickets:
            adj[src].append(dst)

        for key in adj:
            adj[key].sort()

        res = []

        def dfs(src, result, adj):
            if src in adj:
                destinations = adj[src].copy()
                while destinations:
                    dest = destinations[0]
                    adj[src].pop(0)
                    dfs(dest, res, adj)
                    destinations = adj[src].copy()
            res.append(src)

        dfs("JFK", res, adj)
        if len(res) == len(tickets) + 1:
            res.reverse()
            return res
        return False
```


## [778. Swim in Rising Water](https://leetcode.com/problems/swim-in-rising-water/)
### Steps
- Modified Dijkstras
- search neighbors and add to minHeap
	- if nei not in visit then add to heap
	- use max(previous, current) as the value for popping
- when you reach dest return

#### Code
```python
class Solution:
    def swimInWater(self, grid: List[List[int]]) -> int:
        ROW = len(grid)-1
        COL = len(grid[0])-1
        directions=[[0,1], [0,-1], [1,0], [-1, 0]]

        pq = [(grid[0][0], 0, 0)]
        visit = set([(0, 0)])  # Add the starting cell to visited set

        while pq:
            cost, r, c = heapq.heappop(pq)

            if r == ROW and c == COL:
                return cost

            for dr, dc in directions:
                newR, newC = r + dr, c + dc

                if (0 <= newR <= ROW and
                    0 <= newC <= COL and
                    (newR, newC) not in visit):
                    
                    visit.add((newR, newC))  # Mark as visited before adding to queue
                    newCost = max(cost, grid[newR][newC])
                    heapq.heappush(pq, (newCost, newR, newC))

        return -1  # In case no path is found (shouldn't happen for valid inputs)
        
```

# [1135. Connecting Cities With Minimum Cost](https://leetcode.com/problems/connecting-cities-with-minimum-cost/)
### Steps
- Create an adjacency list of all connected vertices
- Traverse the graph by a using a heap
    - add unvisted neighbours to the heap and add their costs
- If the size of the visited set equals n then return the total cost to visit every vertex, else -1

#### Code
```python
class Solution:
    def minimumCost(self, n: int, connections: List[List[int]]) -> int:
        tot = 0
        adj = {i:[] for i in range(1, n+1)}
        for src, dest, cost in connections:
            adj[src].append((cost,dest))
            adj[dest].append((cost,src))
        pq = [(0, connections[0][0])]
        visit = set()

        while pq:
            cost, v = heapq.heappop(pq)

            if v in visit:
                continue
            visit.add(v)
            tot += cost

            for neiCost, nei in adj[v]:
                if nei not in visit:
                    heapq.heappush(pq, (neiCost, nei))

        return tot if len(visit) == n else -1
```

# 
### Steps
* 

#### Code
```python

```


# 
### Steps
* 

#### Code
```python

```


# 
### Steps
* 

#### Code
```python

```

