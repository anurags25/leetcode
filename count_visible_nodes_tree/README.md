## Situation
We're asked to find "visible" nodes of a binary tree. A node is only visible if there's no other node with greater height before it while traversing from root.

## Task
```
Input:
        5
     /     \
   3        10
  /  \     /
20   21   1

Output: 4
Explanation: There are 4 visible nodes: 5, 20, 21, and 10.
```
## Action
Given the visible height threshold(s) for node(s) might be different along each path, we need to explore each path individually. Sounds like a DFS problem!

In each recursion call we need to keep track of the current visible height and if we encounter a node with greater height, mark it and update the visible height (for that particular path, which is implictly taken care of by system's recursion stack).

Here is the code snippet:

```python
def traverse(start, max_height, nodes):
    if start is None:
        return
    if start.val >= max_height:
        max_height = start.val
        nodes.append(start.val)
    traverse(start.left, max_height, nodes)
    traverse(start.right, max_height, nodes)
    return nodes
```

## Results and Rebuttals
Time Complexity: O(N) --> Simple traversal, each node is only visited once.

Do we have to use DFS? Not really, the BFS approach (with same runtime!) is less intuitive but the main idea is the same. At each level, keep track of the visible height along the path traversed by parent.

We can maintain this information right alongside the node in the queue!

Here's the code:

```python
def count_nodes(root):
    visible_nodes = []
    q = deque([(root, root.val)])
    while q:
        node, height = q.popleft()
        if node.val >= height:
            visible_nodes.append(node.val)
        if node.left:
            q.append((node.left, max(node.val, height)))
        if node.right:
            q.append((node.right, max(node.val, height)))
    print (visible_nodes)
    count = len(visible_nodes)
    return count
```
