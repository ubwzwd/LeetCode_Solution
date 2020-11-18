---
description: KMP implementation
---

# LeetCode 28. Implement strStr\(\)

### Question:

| Category | Difficulty | Likes | Dislikes |
| :--- | :--- | :--- | :--- |
| algorithms | Easy \(33.41%\) | 1297 | 1700 |

**Tags**

[`two-pointers`](https://leetcode.com/tag/two-pointers) \| [`string`](https://leetcode.com/tag/string)**Companies**

`apple` \| `facebook` \| `microsoft` \| `pocketgems`

Implement [strStr\(\)](http://www.cplusplus.com/reference/cstring/strstr/).

Return the index of the first occurrence of needle in haystack, or **-1** if needle is not part of haystack.

**Example 1:**

```text
Input: haystack = "hello", needle = "ll"
Output: 2
```

**Example 2:**

```text
Input: haystack = "aaaaa", needle = "bba"
Output: -1
```

**Clarification:**

What should we return when `needle` is an empty string? This is a great question to ask during an interview.

For the purpose of this problem, we will return 0 when `needle` is an empty string. This is consistent to C's [strstr\(\)](http://www.cplusplus.com/reference/cstring/strstr/) and Java's [indexOf\(\)](https://docs.oracle.com/javase/7/docs/api/java/lang/String.html#indexOf%28java.lang.String%29).

### Analyst:

This is a kind of standard implementation of KMP algorithm.

### Solution:

```cpp
class Solution {
    vector<int> calPrefix(string s){
        int n = s.size();
        vector<int> prefix(n,0);
        // calculates the prefix lenth for i-th element, len is the index of element currently be considering add to prefix
        int i = 1, len = 0;
        while(i<n){
            if(s[i] == s[len]){
                len++;
                prefix[i] = len;
                i++;
            }
            // if s[i] != s[len],
            else if(len){
                len = prefix[len-1];
            }
            else{
                prefix[i] = 0;
                i++;
            }
        }
        return prefix;
    }
public:
    int strStr(string haystack, string needle) {
        int len1 = haystack.size();
        int len2 = needle.size();
        if(len2 == 0) return 0;
        // calculate the prefix array
        vector<int> prefix = calPrefix(needle);
        // i is the index in haystack, j is the index in needle
        int i = 0, j = 0;
        while(i < len1){
            if(haystack[i] == needle[j]){
                i++, j++;
            }
            // matched
            if(j == len2){
                return i-j;
            }
            if(i<len1 && haystack[i] != needle[j]){
                if(j > 0)
                    j = prefix[j-1];
                else
                    i++;
            }
        }
        return -1;
    }
};
```

