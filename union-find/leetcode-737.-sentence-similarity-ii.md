# LeetCode 737. Sentence Similarity II

### Question:

| Category   | Difficulty      | Likes | Dislikes |
| ---------- | --------------- | ----- | -------- |
| algorithms | Medium (44.74%) | 409   | 25       |

**Tags**

[`depth-first-search`](https://leetcode.com/tag/depth-first-search) | [`union-find`](https://leetcode.com/tag/union-find)

**Companies**

`Unknown`'\[\["great","good"],\["fine","good"],\["drama","acting"],\["skills","talent"]]'

Given two sentences `words1, words2` (each represented as an array of strings), and a list of similar word pairs `pairs`, determine if two sentences are similar.

For example, `words1 = ["great", "acting", "skills"]` and `words2 = ["fine", "drama", "talent"]`are similar, if the similar word pairs are `pairs = [["great", "good"], ["fine", "good"], ["acting","drama"], ["skills","talent"]]`.

Note that the similarity relation **is** transitive. For example, if "great" and "good" are similar, and "fine" and "good" are similar, then "great" and "fine" **are similar**.

Similarity is also symmetric. For example, "great" and "fine" being similar is the same as "fine" and "great" being similar.

Also, a word is always similar with itself. For example, the sentences `words1 = ["great"], words2 = ["great"], pairs = []` are similar, even though there are no specified similar word pairs.

Finally, sentences can only be similar if they have the same number of words. So a sentence like `words1 = ["great"]` can never be similar to `words2 = ["doubleplus","good"]`.

**Note:**

* The length of `words1` and `words2` will not exceed `1000`.
* The length of `pairs` will not exceed `2000`.
* The length of each `pairs[i]` will be `2`.
* The length of each `words[i]` and `pairs[i][j]` will be in the range `[1, 20]`.

### Solution:

```cpp
#include <vector>
#include <string>
#include <unordered_map>
using namespace std;
// @lc code=start
class UnionFindSet{
    vector<int> ranks_, parents_;
public:
    UnionFindSet(int n){
        ranks_ = vector<int> (n+1,0);
        parents_ = vector<int> (n+1, 0);
        for(int i = 0; i < n+1; i++){
            parents_[i] = i;
        }
    }
    int Find(int u){
        if(parents_[u] != u) parents_[u] = Find(parents_[u]);
        return parents_[u];
    }
    bool Union(int u, int v){
        int uRoot = Find(u);
        int vRoot = Find(v);
        if(uRoot == vRoot) return false;
        if(ranks_[uRoot] > ranks_[vRoot]){
            parents_[vRoot] = uRoot;
        }
        else if(ranks_[vRoot] > ranks_[uRoot]){
            parents_[uRoot] = vRoot;
        }
        else{
            parents_[vRoot] = uRoot;
            ranks_[uRoot]++;
        }
        return true;
    }
};
class Solution {
public:
    bool areSentencesSimilarTwo(vector<string>& words1, vector<string>& words2, vector<vector<string>>& pairs) {
        int len1 = words1.size(), len2 = words2.size(), len = pairs.size();
        if(len1 != len2) return false;
        unordered_map<string, int> index;
        for(int i = 0; i < len; i++){
            index[pairs[i][0]] = i;
            index[pairs[i][1]] = len+i;
        }
        UnionFindSet s(len*2);
        for(const auto& pair : pairs){
            s.Union(index.at(pair[0]), index.at(pair[1]));
        }
        for(int i = 0; i < len1; i++){
            if(words1[i] == words2[i]) continue;
            if(!index.count(words1[i]) ||
                !index.count(words2[i]) ||
                (s.Find(index.at(words1[i])) != s.Find(index.at(words2[i]))))
                return false;
        }
        return true;
    }
};
// @lc code=end
```
