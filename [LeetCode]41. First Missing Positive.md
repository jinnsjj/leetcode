# [41. First Missing Positive](https://leetcode.com/problems/first-missing-positive/description/)

题目要求找出数组中第一个缺失的正数。难点在与时间复杂的要求O(n)，空间复杂度要求O(1)。又是一道不会做抄答案的题目。

思路是把遇到的每一个数放到元数组中排序的位置。

```cpp
class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
        for (int i = 0; i < nums.size(); i++){
            while (nums[i] > 0 && nums[i] < nums.size() && nums[i]!=nums[nums[i]-1])
                swap(nums[i], nums[nums[i]-1]);
        }
        for (int i = 0; i < nums.size(); i++) {
            if (nums[i] != i+1) return i+1;
        }
        return nums.size()+1;
    }
};
```

---

## Reference

> <https://leetcode.com/problems/first-missing-positive/discuss/17071/My-short-c++-solution-O(1)-space-and-O(n)-time>
> <http://www.cnblogs.com/grandyang/p/4395963.html>