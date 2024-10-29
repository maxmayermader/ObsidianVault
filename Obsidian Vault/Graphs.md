#### [[Templates]]

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
        print(adj)
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