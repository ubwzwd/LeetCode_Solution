# LeetCode 139. Word Break

### Quesion

Given a **non-empty** string _s_ and a dictionary _wordDict_ containing a list of **non-empty** words, determine if _s_ can be segmented into a space-separated sequence of one or more dictionary words.

**Note:**

* The same word in the dictionary may be reused multiple times in the segmentation.
* You may assume the dictionary does not contain duplicate words.

**Example 1:**

```text
Input: s = "leetcode", wordDict = ["leet", "code"]
Output: true
Explanation: Return true because "leetcode" can be segmented as "leet code".
```

**Example 2:**

```text
Input: s = "applepenapple", wordDict = ["apple", "pen"]
Output: true
Explanation: Return true because "applepenapple" can be segmented as "apple pen apple".
             Note that you are allowed to reuse a dictionary word.
```

**Example 3:**

```text
Input: s = "catsandog", wordDict = ["cats", "dog", "sand", "and", "cat"]
Output: false
```

### Analysis

{% embed url="http://zxi.mytechroad.com/blog/leetcode/leetcode-139-word-break/" %}

**What's important:**

We just need to go over the left part recursively. For the right part, we just search directly in the dictionary to avoid traverse twice.

### Code

```cpp
#include <unordered_set>
#include <unordered_map>
#include <string>
#include <vector>
using namespace std;
// @lc code=start
class Solution {
    unordered_map<string, bool> map;
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        unordered_set<string> dict(wordDict.begin(), wordDict.end());
        return wordBreakRec(s, dict);
    }

    bool wordBreakRec(const string& s, const unordered_set<string>& dict){
        // if the string has already been visited
        if(map.count(s)) return map.at(s); 
        // if the string is in the dict
        if(dict.count(s)) return map[s] = true;

        // try every break point
        for(int j = 1; j < s.size(); j++){
            // begin at 0, length is j
            const string left = s.substr(0,j);
            // begin at j, to the end
            const string right = s.substr(j);
            if(dict.count(right) && wordBreakRec(left, dict)){
                return map[s] = true;
            }
        }
        return map[s] = false;
    }
};
// @lc code=end
```

