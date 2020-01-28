# Leetcode 39. Combination Sum

### Question:

Given **a set** of candidate numbers \(`candidates`\) \(**without duplicates**\) and a target number \(`target`\), find all unique combinations in candidates where the `candidate` numbers sums to `target`.

The **same** repeated number may be chosen from candidates unlimited number of times.

**Note:**

* All numbers \(including target\) will be positive integers.
* The solution set must not contain duplicate combinations.

**Example1 :**

```cpp
Input: candidates = [2,3,6,7], target = 7,
A solution set is:
[
  [7],
  [2,2,3]
]
```

**Example2 :**

```cpp
Input: candidates = [2,3,6,7], target = 7,
A solution set is:
[
  [7],
  [2,2,3]
]
```

**Hint:**

We can use the backtracking algorithm.

It's similiar to the DFS algorithm, but with some difference In the DFS, we go through every bench to traverse all the elements in the tree. But the backtracking algorithm can go back to the root as soon as we find it impossible.

### Solution:

**Python:**

```text
class Solution:
    def combinationSum(self, candidates, target):
        """
        :type candidates: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        res = []
        candidates.sort()
        self.dfs(candidates, target, res, [])
        return res

    def dfs(self, candidate, target, res, temp):
        if target < 0:
            return
        elif target == 0:
            res.append(temp)
            return
        else:
            for cand in candidate:
                if cand > target:
                    return
                if not temp or cand >= temp[-1]:
                    self.dfs(candidate, target - cand, res, temp+[cand])
        return
```

**C++:**

```cpp
class Solution
{
  public:
    vector<vector<int>> combinationSum(vector<int> &candidates, int target)
    {

        sort(candidates.begin(), candidates.end());
        vector<vector<int>> res = dfs(candidates, target);
        return res;
    }

  private:
    vector<vector<int>> dfs(vector<int> candidate, int target)
    {
        vector<vector<int>> res;
        vector<int> temp;
        dfs_rec(candidate, target, res, temp);
        return res;
    }

    void dfs_rec(vector<int> candidate, int target, vector<vector<int>>& res, vector<int> temp)
    {
        if (target < 0)
            return;
        else if (target == 0)
        {
            res.push_back(temp);
            return;
        }
        else
        {
            for (int i = 0; i < candidate.size(); i++)
            {
                if (candidate[i] > target)
                    return;
                if (temp.size() == 0 || candidate[i] >= temp[temp.size() - 1])
                {
                    vector<int> temp2 = temp;
                    temp2.push_back(candidate[i]);
                    dfs_rec(candidate, target - candidate[i], res, temp2);
                }
            }
        }
        return;
    }
};
```

