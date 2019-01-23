# Leetcode 92. Reverse Linked List II

### Question:

Reverse a linked list from position m to n. Do it in one-pass.

Note: 1 ≤ m ≤ n ≤ length of list.

Example: Input: 1-&gt;2-&gt;3-&gt;4-&gt;5-&gt;NULL, m = 2, n = 4 Output: 1-&gt;4-&gt;3-&gt;2-&gt;5-&gt;NULL

### Solution:

Reverse the "next" pointer. 找到需要反转的那一段，反转里面所有的`next`成员。比如这里，2-&gt;3-&gt;4 变成 4-&gt;3-&gt;2。

然后将1和反转后的头相连，5和反转后的尾相连。

注意，如果是从第一个开始反转，那么反转之后的`head`就是整个链表的`head`，不需要再连了。

这题的重点是记录需要反转的那一段的两头的四个节点，方便最后连接成一个整体。

```cpp
/* *
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * }; */

#include <iostream>

using namespace std;

struct ListNode
{
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

class Solution
{
  public:
    ListNode *reverseBetween(ListNode *head, int m, int n)
    {
        ListNode *original_head = head;
        ListNode *pre_head = NULL;
        for (int i = 1; i < m; i++)
        {
            pre_head = head;    // pre_head is the (m-1)th element
            head = head->next;
        }
        ListNode *after_head = head;    // after_head is the (m)th element
        ListNode *new_head = NULL;  // next_head will be the (n+1)th element
        ListNode *next = NULL;
        ListNode *tail = NULL;  // tail will be the (n)th element
        int change_length = n - m + 1;
        for (int i = 0; i < change_length; i++)
        {
            next = head->next;
            head->next = new_head;
            new_head = head;
            tail = head;
            head = next;
        }
        if (m == 1)
        {
            original_head = tail;
        }
        else
        {
            pre_head->next = tail;
        }
        after_head->next = head;
        return original_head;
    }
};
```

