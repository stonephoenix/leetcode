# backtrack 经常用，此处记其它用法

## 记 grid 中 i 来表示一整行，j...
[51. N-Queens](https://leetcode.com/problems/n-queens/description/) &nbsp;&nbsp; <br/>
[52. N-Queens II](https://leetcode.com/problems/n-queens-ii/description/) &nbsp;&nbsp; 求解法个数 <br/>
[1001. Grid Illumination](https://leetcode.com/problems/grid-illumination/description/) &nbsp;&nbsp; 开灯亮一整行、列、对角、反对解；关灯时关指定及所有近邻共9处灯。求每次关灯前所在位置是否亮着。<br/>
解：memoi 除了记 i 行有灯，还有记有几展，用于关灯时逐一减少。memo[i] += 1, memo[j]+=1, memo[i-j]+=1, memo[i+j]+=1，注意开的时候会重复开，等一些细节。<br/>

[37. Sudoku Solver](https://leetcode.com/problems/sudoku-solver/description/) &nbsp;&nbsp; <br/>
解：注意 inplace 的时候，找到答案后，不能再更改 board 中的元素。<br/>

# Devide & Conquer
[935. Knight Dialer](https://leetcode.com/problems/knight-dialer/description/) &nbsp;&nbsp; 连续N步，状态有重复的，用分治法。<br/>
解: memo[(start, n_jump)] = dict(key=end_point, value=count) <br/>

