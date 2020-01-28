# LeetCode 21. Merge Two Sorted Lists

### Question:

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

Example:

```text
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```

```cpp
// The shape of the listnode:
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
```

### Analysis:

It's a simple problem. Just create a new list and put the smaller one in the head of the two lists into it.

### Solution:

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution
{
  public:
    ListNode *mergeTwoLists(ListNode *l1, ListNode *l2)
    {
        if (!(l1||l2))
            return NULL;
        // creat a new linked list, always put the smaller one in the two lists into this new one.
        ListNode temp{0};
        ListNode *head = &temp;
        while (l1 || l2)
        {
            if (l1 && l2)
            {
                if (l1->val <= l2->val)
                {
                    head->next = l1;
                    l1 = l1->next;
                    head = head->next;
                }
                else
                {
                    head->next = l2;
                    l2 = l2->next;
                    head = head->next;
                }
            }
            else if ((!l1) && l2)
            {
                head->next = l2;
                l2 = l2->next;
                head = head->next;
            }
            else
            {
                head->next = l1;
                l1 = l1->next;
                head = head->next;
            }
        }
        return temp.next;
    }
};
```

