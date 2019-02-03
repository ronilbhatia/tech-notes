## Heaps

*This speaks specifically to min-heaps and binary-heaps*

* A **heap** is a binary tree with certain constraints:
  * Must be a *complete tree*
  * Each node must be >= its parent
    * When a node is added to the tree, if the parent is bigger, the node (value) will be swapped with its parent -> this will be repeated until it is a valid heap
      * How can you be sure after swapping that the other children of the parent will still be valid? Because the swap will only occur if the child is <= the parent, and we know the parent is <= all of its other children (as it was previously a valid heap). Therefore by the transitive property the child must be <= to the other children
  * Gets built top to bottom, left to right, regardless of what values are being added
* Data structure used to implement a *priority queue*
  * Priority queue is a queue that follows FIFO principles, but prioritizes certain items in the queue over others -> the priority is typically represented as an integer where a lower 

### API

* `peek`
  * O(1) time complexity
* `insert`
  * O(log(n)) time complexity
    * The depth of the tree is log(n), since we build the tree top to bottom, left to right. The maximum amount of swaps that occurs due to an insert is the depth of the tree, therefore the time complexity of insertion is O(log(n)). This process of swapping up is called `heapify up`
* `extract` - takes the minimum element(root) and returns it
  * O(log(n)) time complexity
    * Need to restructure tree, switch root element with the bottom, left-most node (the most recently inserted node). Then continue swapping the node with it's smallest child until it is a valid heap. Same reasoning as with `insert` for time complexity - directly related to the depth of the tree. This process of swapping down is called `heapify down`

### Implementation
Heaps can be implemented using *arrays*. Due to the way they are built, you can calculate a node's parent, and children based on the index of the node. See the following table:

| Parent | Children |
|--------|----------|
| 0      | 1, 2     |
| 1      | 3, 4     |
| 2      | 5, 6     |
| 3      | 7, 8     |

* Formula for calculating children based on parent(where **i** is the index of the parent):
  * Left-child: `2i + 1`
  * Right-child: `2i + 2`

* Formula for calculating parent based on child (where **i** is the index of the child:)
  * Parent: `floor((i-1)/2)` - using integer division that formula will work, otherwise make sure to use floor division.

### Heap Sort
Relatively common sort used, though not as popular as quick sort or merge sort.

Steps:
1. `heapify` - iterate through input and `insert` each el into the heap
    * this is an O(nlog(n)) operation as the iteration is O(n), of which each step is a log(n) operation (`insert`)
2. `sort` - iterate through heap and `extract` until the heap is empty.
    * this is an O(nlog(n)) operation for the same reasons as the previous step

#### In-place version
Uses a max heap rather than a min heap.

Steps:
1. Iterate through the array building a max-heap in-place as you go, performing swaps as necessary. 
2. Go backwards through the array, extracting as you go. However, instead of actually removing the elements, just leave them on the end without removing them, but no longer consider them part of the heap as you consider iterating backwards through.

In-place heap sort is ideal for when you are limited on space since it takes up no extra memory(beyond the input array itself)