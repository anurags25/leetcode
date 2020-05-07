## Situation 

We need to write functions to serialize and deserialize a binary tree.

![alt text](https://3.bp.blogspot.com/-T5tlhDPiZnA/V_0INDboDQI/AAAAAAAABS8/je9dgx6_x2Y-AHgoBUQV5RwdaLyuFhPqwCLcB/s1600/serialize-deserialize-binary-tree.png "Question Overview")

## Task 
The question essentially is asking us to convert the tree into a simple(r) data structure and then reconstruct it back. The trick here is to realize that it is as much a *object oriented design* question as it is a data structure/algorithm question.

## Action
To "serialize" the tree we need to use some sort of traversal and use it to deserialize. Let's take inorder traversal.

For the above example, the tree would serialize to [3, 5, 7, 8, 10, 20]. 

To deserialize we just need to figure out where the root is, its left and right child and its left and right child and its left and right child... #classic recursion.

To keep track of this we can maintain the depth information for each node. So the serialized tree would look something like [(3, 2), (5, 1), (7, 3), (8, 2), (10, 0), (20, 1)]. Now all we need to do is connect each node with its children in the next level and we’re done!

## Results and Rebuttals
The time complexity for this approach is O(nlogn), the space complexity is O(n) where n is the number of nodes in the tree.

We don't necessarily have to use inorder traversal, using something like pre-order traversal would result in O(n) time complexity. But as is with most things computer science, there is space-time trade off. This way we need to keep track of the empty nodes too. Not a big difference when we’re dealing with a full(ish) binary tree, but consider an example with an imbalanced linear tree and the number quickly adds up!

## Python Trivia
Python doesn’t have strong public/private distinctions. But using ‘_’ in a function definition indicates that the function is for internal use only! Definitely something to keep in mind if you're asked to design a public facing API in the question.

If you are like me and you use 
```python
if foo:
   #do something
 ``` 
to check if a variable exists. Then here’s something to look out for. The Python interpreter treats 0/1’s as True/False in the if else context. So your if condition doesn’t execute when the variable is 0. This almost led me down the rabbit hole for longer than I’d care to admit!
