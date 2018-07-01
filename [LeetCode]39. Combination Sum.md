# [39. Combination Sum](https://leetcode.com/problems/combination-sum/description/)

题目要求列出所有的可能情况，我也想到了要使用递归去解决，但具体的方法却很头疼，依旧是参考了大佬的答案，豁然开朗<http://www.cnblogs.com/grandyang/p/4419259.html>。

DFS中start变量的引用可以防止递归的答案重复，很优秀。

正如大佬所说，返回所有符合要求的解的题目就想到递归，而思路多相似，要新写一个递归的函数。而这个函数，我们往往会多传入几个变量，来控制循环，记录结果。

---

```cpp
class Solution {
public:
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        vector<vector<int>> res;
        vector<int> out;
        sort(candidates.begin(), candidates.end());
        combinationSumDFS(candidates, target, 0, res, out);
        return res;
    }
    void combinationSumDFS(vector<int>& candidates, int target, int start, vector<vector<int>>& res, vector<int>& out) {
        if (target < 0) return;
        if (target == 0) {
            res.push_back(out);
            return;
        }
        for (int i = start; i < candidates.size(); i++){
            out.push_back(candidates[i]);
            combinationSumDFS(candidates, target-candidates[i], i, res, out);
            out.pop_back();
        }
    }
};
```