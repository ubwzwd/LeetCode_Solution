# LeetCode138 Copy List with Random Pointer

### Question:

A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

Return a deep copy of the list.

```cpp
// The shape of the list node:
/**
 * Definition for singly-linked list with a random pointer.
 * struct RandomListNode {
 *     int label;
 *     RandomListNode *next, *random;
 *     RandomListNode(int x) : label(x), next(NULL), random(NULL) {}
 * };
 */
```

### Analysis:

The main problem is how to copy the "random" field in the linked list.

My idea is to store the index and the address of the nodes in a map. Then I can find the index of the "random" node through its address.

The map is like a `map<RandomListNode *, int> node_map;`.

The new linked list can be stored in a `vector` so that the index is given normally and we don't need to store it in a new map again. 

### Solution:

```cpp
/**
 * Definition for singly-linked list with a random pointer.
 * struct RandomListNode {
 *     int label;
 *     RandomListNode *next, *random;
 *     RandomListNode(int x) : label(x), next(NULL), random(NULL) {}
 * };
 */
class Solution
{
  public:
    RandomListNode *copyRandomList(RandomListNode *head)
    {
        if (head)
        {
            // to store the location and its index of the old list
            map<RandomListNode *, int> node_map;
            // to store the location of every node in the new list
            vector<RandomListNode *> node_vec;
            RandomListNode *ptr = head;
            int i = 0;
            while (ptr)
            {
                // put the new node in the vector and initialize its label
                node_vec.push_back(new RandomListNode(ptr->label));
                // put the old node into the map
                node_map[ptr] = i;
                // move to the next node in the old list
                ptr = ptr->next;
                i++;
            }
            ptr = head;
            // get the real size of the vector, not the max index
            int len = i;
            // when allocate the "next" field, we need one more node
            //node_vec.push_back(0);
            i = 0;
            // link the new list
            while (ptr)
            {
                // allocate the "next" field
                if (i != len - 1)
                    node_vec[i]->next = node_vec[i + 1];
                // allocate the "random" field
                if (ptr->random)
                {
                    // get the index of the next node
                    int next_index = node_map[ptr->random];
                    node_vec[i]->random = node_vec[next_index];
                }
                ptr = ptr->next;
                i++;
            }
            return node_vec[0];
        }
        else{
            return NULL;
        }
    }
};
```

