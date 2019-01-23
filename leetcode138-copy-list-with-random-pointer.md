# LeetCode138 Copy List with Random Pointer

### Question:

A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

Return a deep copy of the list.

### Analysis:

The main problem is how to copy the "random" field in the linked list.

My idea is to store the index and the address of the nodes in a map. Then I can find the index of the "random" node through its address.

The new linked list can be stored in a `vector` so that the index is given normally and we don't need to store it in a new map again. 

