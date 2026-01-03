# Summary of Recursion

## Key Point

1. Base case: the smallest problem to solve directly
2. Recursive rule: how to make the problem smaller, and in the end we can use the result of the base case.

## Types

### Recursion with Number

#### a^b

\= a \* (a^(b-1))

....

Base case: a \* a

Recursive rule: take 1 `a` out of the multiplication.

### Recursion with Array

#### 1-D array

merge sort, quick sort

#### 2-D (or above) array

DFS

### Recursion with LinkedList

#### Reverse LinkedList

#### Reverse LinkedList by Group

### Recursion with Tree

#### Base case:

the relation of the parent, the children and a node itself.

#### Recursion rule:

1. what do you want from your children
2. what do you want to do in the current node
3. what do you want to return to your parent

#### Examples:

LCA

check if a tree is balanced

successor in a BST

Implement Heap: percolate down, percolate up

### Recursion with String

#### Type1: similar as 1-D array

#### Type2: Make use of the semantics

example: abbrevation

check if a string matches the abbrevation

eg. string is `kubernetes` , abbr is `k8s` , `k3r4s` (match)

base case: string, abbr

`"" == ""`  &#x20;

&#x20;`(!"") != ""`  &#x20;

`"" != (!"")` &#x20;

`{char} == {char} or substring.length() == number`&#x20;

recursive rule: match recursively from left to right
