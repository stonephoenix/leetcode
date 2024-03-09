#一般为排列组合类问题，通过剪枝 O(2^N) -> O(2^K)

## 括号问题: 
### 性质1: 右括号一多，即可判定 invalid，左括号多，需要到最后才能判定。
### 性质2: invalid 的情形只能是 左区间 s[0:k+1] 右括号多，右括号多的右边界需要在每次碰到)时就更新；右区间 s[k+1:] 左括号多

[2267. Check if There Is a Valid Parentheses String Path](https://leetcode.com/problems/check-if-there-is-a-valid-parentheses-string-path/description/) &nbsp;&nbsp 二维，性质1 <br/>
解：题意较简单，但 DFS + early stop 仍需要 2^((m+n)//2) 复杂度；使用DP更快，前一状态最多(m+n)//2个left，复杂度为 m*n*((m+n)//2)。

[921. Minimum Add to Make Parentheses Valid](https://leetcode.com/problems/minimum-add-to-make-parentheses-valid/description/) &nbsp;&nbsp 性质2 <br/>
[1249. Minimum Remove to Make Valid Parentheses](https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/description/) &nbsp;&nbsp 性质2, 碰到多的 ) 不 append 到结果中，最后从右往左，删除多余的左括号个数<br/>
[1963. Minimum Number of Swaps to Make the String Balanced](https://leetcode.com/problems/minimum-number-of-swaps-to-make-the-string-balanced/description/) &nbsp;&nbsp 性质2, swap 一次可解决两个imbalance问题<br/>
[2116. Check if a Parentheses String Can Be Valid](https://leetcode.com/problems/check-if-a-parentheses-string-can-be-valid/description/) &nbsp;&nbsp 位置上有01标识是否可以flip，问能否变成valid<br/>
解：从左往右，) 多的时候，检查是否有可 flip 的 (，可以实现左区间 valid；右区间使用 从右往左 扫描的方法。<br/>
[301. Remove Invalid Parentheses](https://leetcode.com/problems/remove-invalid-parentheses/) &nbsp;&nbsp 移除最少的多余括号，并返回所有可能结果<br/>
解：先找到右括号多的右边界 rightmost_boundary 以及多的个数，再找到左括号多的个数，backtrack，rightmost_boundary 之前可删除或者保留右括号，之后可删除或保留左括号。