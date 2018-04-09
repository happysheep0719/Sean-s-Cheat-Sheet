<extoc></extoc>

# Graph

**Graph** can be represented using **Adjacency Matrix** and **Adjacency List**.

Following is an example undirected graph with 5 vertices.

![Graph](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/undirectedgraph.png)

![Adjacency Matrix](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/adjacencymatrix.png)

![Adjecency List](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/listadjacency.png)

## Generic Tree Search Algorithm (BFS and DFS)

Reference - [USC-CSCI561-Lecture-Week2]

```c
function TREE_SEARCH(problem) return a solution or failure

frontier <- MAKE_QUEUE(MAKE_NODE(problem.INITIAL_STATE))
loop do
    if ISEMPTY(frontiers) then return failure
    node <- REMOVE_FIRST(frontiers)
    if problem.GOAL_TEST() applied to node.STATE succeeds
        then return SOLUTION(node)
    frontiers <- INSERT_ALL(EXPAND(node, problem), frontiers)
```

__Note:__

- Always remove elements from the front
- BFS places new elements at the end of the queue. FIFO.
- DFS places new elements at the front of the queue(stack). LILO.