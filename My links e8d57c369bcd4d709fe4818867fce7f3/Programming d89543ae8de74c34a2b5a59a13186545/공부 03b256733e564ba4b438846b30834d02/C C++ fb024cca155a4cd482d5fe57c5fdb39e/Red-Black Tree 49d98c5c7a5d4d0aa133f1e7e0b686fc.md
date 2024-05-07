# Red-Black Tree

Red Black Tree is also a balanced BST tree that guarantees the time complexity of $O(log_2(n))$ for insertion/deletion/search. But doesn’t AVL Tree do the same as well? Why do we need the Red Black Tree? That is because Red Black Tree requires only up to two rotation (at max), while AVL Tree sometimes requires a lot of rotations in case of complex BST. 

AVL Tree is a strict height balanced tree. Red Black Tree roughly balance height compared to AVL Tree. all AVL Trees are Red-Black Tree. All the Red-Black Trees, however, aren’t AVL Tree.

$AVL\ \ Tree \subseteq Red -Black \ \ Tree$

 This means…

- insertion/deletion is faster → $Red-Black \ \  Tree$
- search is faster → $AVL \ \ Tree$

**characteristics of Red-Black Tree**

- it is a self-balancing BST
- Every node is either Black or Red
- Root is always Black
- Every leaf which is Nil is Black
- if node is Read then its children are always Black
- Every path for a node to any of its descendent Nil node has same no. of Black nodes
- the length of the farthest path of the red-black tree cannot be greater than twice the nearest path of the tree. (counting the nils)
- insertion
    
    
- deletion