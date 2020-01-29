# LeetCode 684. Redundant Connection

### Question:

| Category | Difficulty | Likes | Dislikes |
| :--- | :--- | :--- | :--- |
| algorithms | Medium \(55.02%\) | 943 | 216 |

**Tags**

[`tree`](https://leetcode.com/tag/tree) \| [`union-find`](https://leetcode.com/tag/union-find) \| [`graph`](https://leetcode.com/tag/graph)**Companies**

`google`

In this problem, a tree is an **undirected** graph that is connected and has no cycles.

The given input is a graph that started as a tree with N nodes \(with distinct values 1, 2, ..., N\), with one additional edge added. The added edge has two different vertices chosen from 1 to N, and was not an edge that already existed.

The resulting graph is given as a 2D-array of `edges`. Each element of `edges` is a pair `[u, v]` with `u < v`, that represents an **undirected** edge connecting nodes `u`and `v`.

Return an edge that can be removed so that the resulting graph is a tree of N nodes. If there are multiple answers, return the answer that occurs last in the given 2D-array. The answer edge `[u, v]` should be in the same format, with `u < v`.

**Example 1:**  


```text
Input: [[1,2], [1,3], [2,3]]
Output: [2,3]
Explanation: The given undirected graph will be like this:
  1
 / \
2 - 3
```

**Example 2:**  


```text
Input: [[1,2], [2,3], [3,4], [1,4], [1,5]]
Output: [1,4]
Explanation: The given undirected graph will be like this:
5 - 1 - 2
    |   |
    4 - 3
```

**Note:**  


The size of the input 2D-array will be between 3 and 1000.

Every integer represented in the 2D-array will be between 1 and N, where N is the size of the input array.

### Analysis:

We can use Union Find Directly.

### Solution:

```cpp
#include <vector>
#include <unordered_set>
using namespace std;
// @lc code=start
class UnionFindSet{
private:
    vector<int> ranks_, parents_;
public:
    UnionFindSet(int n){
        ranks_ = vector<int>(n+1, 0);
        parents_ = vector<int>(n+1, 0);
        for(int i = 0; i < parents_.size(); i++){
            parents_[i] = i;
        }
    }
    bool Union(int u, int v){
        int uRoot = Find(u);
        int vRoot = Find(v);
        if(vRoot == uRoot) return false;
        if(ranks_[uRoot] < ranks_[vRoot])
            parents_[uRoot] = vRoot;
        else if(ranks_[uRoot] > ranks_[vRoot])
            parents_[vRoot] = uRoot;
        else // uRoot == vRoot
        {
            parents_[uRoot] = vRoot;
            ranks_[vRoot]++;
        }
        return true;
    }
    int Find(int u){
        if(parents_[u] != u){
            parents_[u] = Find(parents_[u]);
        }
        return parents_[u];
    }
};

class Solution {
public:
    vector<int> findRedundantConnection(vector<vector<int>>& edges) {
        UnionFindSet s(edges.size());

        for(const auto& edge : edges){
            if(!s.Union(edge[0], edge[1]))
                return edge;
        }
        return {};
    }
};
// @lc code=end
```

