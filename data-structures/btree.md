## BTree

**A data structure well-suited for storage systems that read and write relatively large blocks of data, such as hard discs**

### Properties
* Each node can store a pre-defined maximum number of keys(**2d**), which are sorted and act as separator valuese by which the rest of the tree (i.e. its children) are sorted.
* At a minimum, a node should maintain half of its maximum # of keys. Therefore the range of the node's # of keys is **(d-2d)**
* The minimum branching factor of the tree is **(d+1)**, where **d** is the minimum # of keys.
  * Note that minimum # of keys constraint does not apply to the root node (or you'd never be able to insert your first element if your max # of keys is anything greater than two)
* All leaves in a btree must live at the same depth.

### Uses
* Commonly used in database storage and file systems for its ability to:
  * keep keys in sorted order for sequential traversing
  * use hierarchical index to minimize the number of disc reads
  * use partially full blocks to speed insertions and deletions (cost of restructuring tree is expensive)
  * keeps index balanced with recursive algorithm
