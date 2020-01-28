# LeetCode 25. Reverse Nodes in k-Group

### Question:

Given a linked list, reverse the nodes of a linked list _k_ at a time and return its modified list.

_k_ is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of _k_ then left-out nodes in the end should remain as it is.

Example:

Given this linked list: `1->2->3->4->5`

For _k_ = 2, you should return: `2->1->4->3->5`

For _k_ = 3, you should return: `3->2->1->4->5`

Note:

* Only constant extra memory is allowed.
* You may not alter the values in the list's nodes, only nodes itself may be changed.

### Analysis:

This is different from the swap two nodes. We should take the integer `k` into account.

The first way is to reverse the nodes in groups of k, similar as the steps in swap two nodes. We should reverse k nodes at a time. Every time we reverse, we put the last nodes in this group to head. When the original head becomes the tail of this group, this group reverse is done.

```text
-1->1->2->3->4->5
 |        |  |
pre      cur next

-1 ->1 -> 2->3->4->5
|    |    |       |
pre last cur     next

-1->2-> 1->3->4->5
 |      |  |     |
 pre  last cur  next
 
 -1->2-> 1->3->4->5
 |       |  |     |
 pre   last cur  next
 
-1->3->2->1 ->  4->5
 |        |     |   
 pre     last cur&next

-1->3->2->1->4->5
          |  |
         pre next
```

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
  private:
    // swap p and p+1
    ListNode *swapOneGroup(ListNode *pre, ListNode *nex)
    {
        ListNode * last = pre->next;
        ListNode * cur = last->next;
        while(cur!= nex)
        {
            last->next = cur->next;
            cur->next = pre->next;
            pre->next = cur;
            cur = last->next;
        }
        //return the last node, all nodes are coinnected already
        return last;
    }
  public:
    ListNode *reverseKGroup(ListNode *head, int k)
    {
        if(head == NULL || k == 1) return head;
        int len = 0;
        ListNode * res = new ListNode{0};
        res->next = head;
        // current: node 0, pre: before head, next: node 1
        ListNode * current = head, *pre = res, *nex = head->next;
        // get the length of the linked list
        while(current)
        {
            current = current->next;
            len+=1;
        }
        current = head;
        for(int i = 1; i<=len;i++)
        {
            if(i%k==0)
            {
                nex = current->next;
                pre = swapOneGroup(pre, nex);
                current = pre->next;
            }
            else
            {
                current = current->next;
            }
            
        }
        return res->next;
    }
};
```

