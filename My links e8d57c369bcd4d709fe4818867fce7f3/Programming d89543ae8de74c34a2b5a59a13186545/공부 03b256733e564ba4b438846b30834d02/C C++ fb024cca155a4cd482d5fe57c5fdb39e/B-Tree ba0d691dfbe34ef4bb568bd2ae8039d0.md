# B-Tree

- balanced m-way tree (m means the order of tree)
- always grows towards root
- insertion is always on the leaf nodes
- generalization of BST in which a node can have more than one key & more than 2 children
- maintains sorted data
- all leaf node must be at the same level
- B_tree of order $m$ has following properties:
    
    → Every node has  at max m children
    
    → Min children: for leaf → 0
    
                          for root → 2
    
                          for internal nodes → $\frac{m}{2}$ (ceil)
    
    → Every node has max $(m-1)$keys
    
    → Min keys: for root → 1
    
                         for others → $\frac{m}{2}-1$
    

$create \ a\ B-tree\ of\ order\ 3\ by\ inserting\ values\ from\ 1\ to\ 10.$

$create\ a\ B-tree\ of\ order\ 5\ by\ inserting\ values\ from\ 1\ to\ 20$.

$contruct\ a\ B-tree\ of\ order\ 5\ with\ the \ following\ set\ of\ data \newline$D, H, Z, K, B, P, Q, E, A, S, W, T, C, L, N, Y, M

$construct\ a\ B-tree\ of\ order\ 4\ with\ following\ set\ of\ data$

5, 3, 2, 1, 9, 1, 13, 2, 7, 10, 12, 4, 8