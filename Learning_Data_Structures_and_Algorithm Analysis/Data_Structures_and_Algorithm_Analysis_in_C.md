



# Chapter 4:  Trees



The data structure that we are referring to is known as a `binary search tree`. 



## 4.1  Preliminaries



### 4.1.1  Implementation of Trees

One way to implement a tree would be to have in each node, besides its data, a pointer to each child of the node. However, since the number of children per node can vary so greatly and is not known in advance, it might be infeasible to make the children direct links in the data structure, because these would be too much wasted space. The solution is simple: Keep the children of each node in a linked list of tree nodes. The declaration in **Figure 4.3** is typical.

**Figure 4.4** shows how a tree might be represented in this implementation. Arrows that point downward are `FirstChild` pointers. Arrows that go left to right are `NextSibling` pointers. `NULL` pointers are not drawn, because there are too many. 

In the tree of **Figure 4.4**, node *E* has both a pointer to a sibling(F) and a pointer to a child(I), while some nodes have neither.

>   ~~~c
>   typedef struct TreeNode *PtrToNode;
>
>   struct TreeNode
>   {
>   	ElementType Element;
>   	PtrToNode FirstChild;
>   	ptrToNode NextSibling;
>   }
>   ~~~
>   **Figure 4.3**  Node declarations for trees 



>   <img src=".\img\4_4.jpg" style="height:280px">     
>
>   **Figure 4.4**  First child/next sibling representation of the tree shown in *Figure 4.2*