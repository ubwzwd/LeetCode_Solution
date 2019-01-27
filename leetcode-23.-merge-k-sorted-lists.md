# LeetCode 23. Merge k Sorted Lists

### Question:

Merge _k_ sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

Example:

```text
Input:
[
  1->4->5,
  1->3->4,
  2->6
]
Output: 1->1->2->3->4->4->5->6
```

```cpp
// The shape of ListNode:
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

In this question, we are told to merge k lists. There is two different ways.

1. Using a map to include all the value-address pair. Put all values in a vector and sort them, then find their address and link them. Here we may need to store multiple addresses according to one value.
2. Merge sort. When things come to that we need multiple steps to solve multiple similar tasks, we consider iteration and recurrence.

In this problem, I choose merge sort because I've already done with 2 lists merge.

### Solution:

```cpp
class Solution
{
  public:
    ListNode *mergeKLists(vector<ListNode *> &lists)
    {
        // merge sort
        if (lists.size() == 0)
        {
            return NULL;
        }
        if (lists.size() == 1)
        {
            return lists[0];
        }
        if (lists.size() == 2)
        {
            return mergeTwoLists(lists[0], lists[1]);
        }
        int mid = lists.size() / 2;
        // merge
        vector<ListNode *> sub_list1;
        vector<ListNode *> sub_list2;
        int i;
        for (i = 0; i <= mid; i++)
        {
            sub_list1.push_back(lists[i]);
        }
        for (i = mid+1; i < lists.size(); i++)
        {
            sub_list2.push_back(lists[i]);
        }
        ListNode* head1 = mergeKLists(sub_list1);
        ListNode* head2 = mergeKLists(sub_list2);

        return mergeTwoLists(head1, head2);
    }

    ListNode *mergeTwoLists(ListNode *l1, ListNode *l2)
    {
        if (!(l1 || l2))
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

