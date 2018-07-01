# [38. Count and Say](https://leetcode.com/problems/count-and-say/description/)

这题最开始题目没看懂。看懂后发现和Cracking the Coding Interview里面的字符串压缩的题目（1.6）很像，就是计算一个数字重复几次，然后打印重复的数量和该数字。
在字符串压缩的题目中，我用了好几个if判断，这次看了<http://www.cnblogs.com/grandyang/p/4086299.html>把循环优化为while，代码要简洁不少。

```cpp
class Solution {
public:
    string countAndSay(int n) {
        if(n <= 0 ) return "";
        string last = "1";
        while(--n){
            string cur = "";
            for (int i = 0; i < last.size(); i++){
                int cnt = 1;
                while (i+1<last.size() && last[i]==last[i+1]){
                    cnt++;
                    i++;
                }
                cur += to_string(cnt)+last[i];
            }
            last = cur;
        }
        return last;
    }
};
```