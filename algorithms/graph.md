<extoc></extoc>

# Graph

## Representation

**Graph** can be represented using **Adjacency Matrix**, **Adjacency List** and **hash table**.

Following is an example undirected graph with 5 vertices.

![Graph](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/undirectedgraph.png)

![Adjacency Matrix](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/adjacencymatrix.png)

![Adjecency List](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/listadjacency.png)

__Adjacency Matrix vs. Adjacency Lists__

- Adjacency Matrix
    - Time: Edge removal $$O(1)$$, Query of Edge $$O(1)$$
    - Space: $$O(V^2)$$
- Adjacency List
    - Time: Query of Edge $$O(V)$$
    - Space: $$O(V + E)$$


## Graph Search Algorithms

__Draw the Search Graph of Problems__

- What does it store on each level?
- How many different states should we try to put on each level?

### Breadth-First Search (BFS-1)

__Problems__

__P1. Level order treverse__

__P2. Bipartite__

The graph can be divided into two parts, in either of  which there is no direct edges between nodes.

![Bipartite Graph](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e8/Simple-bipartite-graph.svg/440px-Simple-bipartite-graph.svg.png)

- use two explored sets
- make sure nodes of two consequent levels do not have nodes in common.

__P3. Determine whether a binary tree is a complete binary tree__

- find the first node that misses one or two children node.
- ensure the nodes behind have no child.

### Best-First Search (BFS-2)

Dijkstra's algorithm

__Problems__

__P1. find the shortest path cost from source node to  any other nodes in the graph__

- 点到面
- 使用Min Heap记录candidates
- Any node can only be expanded once but can be generated more than once.

### Depth First Search (DFS, Back-tracking) 

- Draw recursion tree
    - How many levels are there?
    - How many branches can we make from the current code
- **Tricks**
    - **inplace**
        - **split the input array into two parts** by using **`swap`**
            - `Arranged characters | Candidate characters`
        - use two resizable container respectively record the arranged charcters and candidate charcters**. In Java, use `StringBuilder` to record arranged characters and use `Set`/`List`/`boolean[]` to record candidates.
    - **remove duplicate**
        - **sort the array first then use a while loop to move index **in each function call
        - use extra space like `HashSet` in Java to record used characters in each level

#### P1. subsets

#### P2. make up 99 cents with 4 kinds of coins
    - 4 levels in total

#### P3. 

#### P4. Permutations

### Generic Tree Search Algorithm (BFS and DFS)

Reference - [USC-CSCI561-Lecture-Week2]

__Three points__

- Initial state
- Expansion/generation rule
- Termination condition

```c
function TreeSearch(problem) return a solution or failure

frontier <- makeQueue(makeNodes(problem.INITIAL_STATE))
loop do
    if isEmpty(frontiers) then return failure
    node <- removeFirst(frontiers)
    if goalTest() applied to node.state succeeds
        then return solution(node)
    frontiers <- insertAll(EXPAND(node, problem))
```

__Expand Function__

```python
// @Return: a set of nodes
def expand(node, problem):
    successors = set([])
    for (action, result) in problem.get_successors(node.state):
        s = node(empty)
        s.state = result
        s.parent_node = node
        s.action = action
        s.path_cost = node.path_cost + get_step_cost(node, action, s)
        s.depth = node.depth + 1
        successors.add(s)
    return successors

```


__Note:__

- Always remove elements from the front
- BFS places new elements at the end of the queue. FIFO.
- DFS places new elements at the front of the queue(stack). LILO.

### Generic Graph Search Algorithm

```c
function GraphSearch(problem) return a solution or failure

frontier <- makeQueue(makeNodes(problem.INITIAL_STATE))
exploredSet <- empty // change 1
loop do
    if isEmpty(frontiers) then return failure
    node <- removeFirst(frontiers)
    if goalTest() applied to node.state succeeds
        then return solution(node)
    exploredSet <- insert(node, exploredSet) // change 2; after goalTest the node.
    candidateNodes <- EXPAND(node, problem)
    candidateNodes.filter(NOT in frontier && NOT in exploredSet)
    frontiers <- insertAll(candidateNodes)
```

## Topological Sorting 拓扑排序