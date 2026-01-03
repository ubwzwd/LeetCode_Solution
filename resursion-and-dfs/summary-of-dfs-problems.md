# Summary of DFS problems

## Type1: subset

### Original Problem

#### Description:

Given an array of unique characters. Return all the subsets of this array.

#### Solution:

eg. \["a", "b", "c"]

&#x20;                              ""

&#x20;                       /              \\

&#x20;                "a"                       ""

&#x20;              /      \                  /       \\

&#x20;    "ab"            "a"         "b"        ""

&#x20;   /     \            /   \        /   \       /   \\

"abc" "ab" "ac" "a" "bc" "b"  "c"   ""

### Variant 1

#### Description:

Given an array of unique characters. Return all the subsets of this array whose size is equal to k.

#### Solution:

difference: more restraint on when to return. Need to return when we finish traversing the whole array or the subset size is already k.

### Variant 2

#### Description:

Given an array of characters. Return all the subsets of this array.

The elements in this array may be duplicated. Note that the duplicated characters are considered the same.

#### Solution:

eg. \["a", "b", "b", "b", "c"]

method 1: Same as original problem. Add a set `s` to remove duplicates.

\["a", "b", "b"] ==> "a|b|b" ==> if this string is in `s`? ==> if so, skip. If not, add it to `s and add this subset to the result.`

&#x20;                                   ""

&#x20;                             /              \\

&#x20;                      "a"                       ""

&#x20;                    /      \                  /       \\

&#x20;              `ab1    a      b1   ""`

&#x20;     `/  \   /  \   /  \  /  \`

&#x20; `ab1b2 ab1 ab2 a b1b2 b1 b2 ""`&#x20;

**method 2: remove duplicates when doing DFS**

**Important: ensure the array is sorted**

\["a", "b1", "b2", "b3", "c"]

&#x20;                                               ""

&#x20;                                        /                  \\

&#x20;                               "a"                            ""

&#x20;                    /    |       |        \                  /       \\

&#x20;              `ab abb abbb   a     b bb bb ""`

&#x20;     `/  \   /  \   /  \  /  \`

&#x20;                                 `... for c`

## Type2: Parenthesis

### Original Problem

Given n pairs of parenthesis, provide all the valid combinations.

#### Analysis

For example, `n = 3`

All valid combinations are:

`((()))`, `(())()`, `()(())`, `()()()`

invalid example: `())(`

If the final string is s, for any i (i < n \* 2), the number of left parentheses is greater than the number of right ones in s\[0, i].

mid-level solution:\
1\. how many levels of recursion: 2n, decide what kind of parenthesis to put in each position in the corresponding level

2\. how many branches there are on each level: 2, if the existing left parenthesis is more than right ones. Otherwise we have only 1 choice.

How to check the number of used left/right parenthesis: use a integer, right = -1, left = +1, keep the number >= 0

Time complexity: 2^(2n) = 4^n

Space complexity: 2n (running mem cost) + 2n \* 4^n (mem cost to store result)&#x20;

### Variant 1

m {}, n \[], k (), no priority

Valid results: `{[()]}`, `([{}])`

Invalid: `{[(])}`

How to check: use a stack, add left parenthesis on, and delete it when it's on the top and we add a right parenthesis.

### Variant 2

m {}, n \[], k (), has priority, {} > \[] > ()

Valid results: `{[()]}`

Invalid: `([{}])`

One more thing to check when we add left ones: we can only add `[` and `(` if the top of stack is a `[`.

## Type3: Duplicate combination

### Original Problem

Given a target number `n`, you are required to use coins with certain amounts of `a`, `b` and `c` to sum up to `n`. Please note that you can use unlimited numbers of each kind of coin.

#### Analysis

n = 99, coins = 1, 2, 5

**Method 1**

DFS

1. what does each level represent: which coin we are adding to the result.
2. how many level in total: in each level, we put 1 coin. So in total, the max level will be 99 (`n/min(a, b, c)`)

Time complexity: `O(3^99)` &#x20;

Space complexity: `O(3^99)`

**Method 2**

DFS

1. What does each level represent: in each level, we will use 1 type of coin. And will try all the possible numbers of the specific coin. Each level has max 99 choices (`n/min(a, b, c)`)
2. how many levels in total: 3

Time complexity: `O(99^3)`&#x20;

Space complexity: `O(99^3)`&#x20;

## Type4: Permutation

### Original Problem

Given a string `s` (without duplicate letters inside), return all the permutations

#### Analysis

`abc` ,

permutations: `abc`, `acb`, `bac`, `bca`, `cab`, `cba`&#x20;

Method: swap the first element with each of the following

1. What does each level represents: the letter to put in the index, each level has at most `s.length()` choices
2. how many levels in total: `s.length()`

Time complexity: `O(s.length() ^ s.length()) ==> O(s.length()!)`&#x20;

Space complexity: `O(s.length())`&#x20;

### Variant 1

Given a string `s` (with duplicate letters inside), return all the permutations

#### Analysis

Same as origin

How to deduplicate:

add a HashSet()

1. add the HashSet at the very beginning and only use one HashSet. Store the whole string in the set. Space complexity: `O(s.length()!)`&#x20;
2. use a new HashSet at each recursion level. Store the used letter in the current index into the set. Space complexity: `O(s.length() ^ 2)`&#x20;

