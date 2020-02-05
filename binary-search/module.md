# Module

Reference to the C++ &lt;algorithm&gt; library, "lower\_bound" function.

```cpp
// given a vector a[], an integer target
int binarySearch(vector<int> a, int target){
    int left = 0, right = n;
    while(left < right){
        mid = left+(right-left)/2;
        if(a[mid] < target) left = mid+1;
        else right = mid;
    }
    // left is the first element not less than target
    return left;
}
```

The stop requirement of the while loop is either left = right. So return left or right are both OK.

The left is the first one no less than target.

If we want upper bound

```cpp
// given a vector a[], an integer target
int binarySearch(vector<int> a, int target){
    int left = 0, right = n;
    while(left < right){
        mid = left+(right-left+1)/2;
        if(a[mid] > target) right = mid-1;
        // a[mid] <= target
        else left = mid;
    }
    return left;
}
```



