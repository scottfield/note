###Tree
* binary tree
* binary search tree
* AVL tree O(Logn)
* red black tree O(Logn)
    
    rules:
    1) Every node has a color either red or black.
    2) Root of tree is always black.
    3) There are no two adjacent red nodes (A red node cannot have a red parent or red child).
    4) Every path from a node (including root) to any of its descendant NULL node has the same number of black nodes.
* B tree


###Heap(MinHeap or MaxHeap)
properties:
- it's a complete binary tree(all nodes arranged from top to bottom and left to right)
- anyone node's value are greater than or equal to(less than or equal to) all of its children nodes.

we often use an array to implement heap, here are relationship between array index and node index
###the heap index start with 1
###how to find a node's parent node?
 parentNodeIndex = currentNodeIndex/2 
###how to find a node's left and right child nodes?
leftChildNodeIndex=currentNodeIndex*2
rightChildNodeIndex=currentNodeIndex*2+1

###how to determine if a node is leaf node or not?
it's a leaf node:currentNodeIndex >n/2
it's not a leaf node:currentNodeIndex<=n/2

n is the total elements of the heap
### Static array
### Dynamic array
### Linked list
### Set
### Hashing
#### Hash function type
- division hash(simply modular)
- universal hash(choose a dynamic factor to evenly calculate hash slot)
#### Hash collision handling
- open addressing(the hashtable itself store the data,e.g. linear probing,quadratic probing, second hash etc.)
- separate chain(e.g. indirectly use array, linked list,dynamic array etc. to store data in the hash table)
