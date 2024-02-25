# Jump Game
[55. Jump Game](https://leetcode.com/problems/jump-game/description/)&nbsp;&nbsp;只能向右最多跳 nums[i] 步，i 为当前点，求是否能到终点<br/>

[45. Jump Game II](https://leetcode.com/problems/jump-game-ii/description/)&nbsp;&nbsp;只能向右最多跳 nums[i] 步，i 为当前点，求最快几步到终点<br/>
解：一路向右跳，每轮跳到前一轮最右标记 <br/>

[1306. Jump Game III](https://leetcode.com/problems/jump-game-iii/description/)&nbsp;&nbsp;可左右跳 nums[i] 步，i 为当前点，要求跳到值为0的点<br/>
解：BFS 染色 <br/>

[1345. Jump Game IV](https://leetcode.com/problems/jump-game-iv/description/)&nbsp;&nbsp;大富翁，可前后跳一步，或者跳到与当前值相同的地点，求多少步能跳到终点 <br/>
解：双向 BFS <br/>
注意：跳到与当前值相同的点，用过一次之后，不需要再跳，通常的做法是先尝试跳，然后根据染色标记直接返回，但这样仍然需要有很多次尝试（K-1平方 复杂度，K为相同值的地点个数，每个地点都需要尝试 K-1 次），因此最便捷的方法是，用过一次这种跳法后，在 hashtable 中把这个信息删掉。

[1340. Jump Game V](https://leetcode.com/problems/jump-game-v/) &nbsp;&nbsp;窗口范围内只能往低跳 <br/>
解：DP，从最低点往高处跳，max(all possible steps)

[1696. Jump Game VI](https://leetcode.com/problems/jump-game-vi/description/) &nbsp;&nbsp;最近窗口最大值<br/>
解：递增/递减 队列

[1871. Jump Game VII](https://leetcode.com/problems/jump-game-vii/) &nbsp;&nbsp;往前跳 最少M步，最多N步，当前值为0时才能继续跳<br/>
解：DP，染色

[2297. Jump Game VIII](https://leetcode.com/problems/jump-game-viii/description/) &nbsp;&nbsp;每个数的 下一个更大/小值<br/>
解：递增/递减 队列，在每次 pop 后增加比较的操作
     ___4 3 2 1 3 5 <br/>
     ___[4 3 2 1]\(3) -> [4 3]\(3) -> [4 3 3]<br/>
     idx[0 1 2 3]\(4) -> [0 1]\(4) -> [0 1 4]<br/>
     ___[4 3 3]\(5) ->[4 3]\(5) -> [4]\(5) -> []\(5) -> [5]<br/>
     idx[0 1 4]\(5) ->[0 1]\(5) -> [0]\(5) -> []\(5) -> [5]<br/>

# Unique Path
[62. Unique Paths](https://leetcode.com/problems/unique-paths/description/)&nbsp;&nbsp; grid 左上角至右下角，只能向右或向下，有多少种走法<br/>
解：grid[i][j] = grid[i-1][j] + grid[i][j-1]，再优化成一行DP <br/>

[63. Unique Paths II](https://leetcode.com/problems/unique-paths/description/)&nbsp;&nbsp; 62基础上增加 block cell

[980. Unique Paths III](https://leetcode.com/problems/unique-paths-iii/description/)&nbsp;&nbsp; 4个方向走，带block cell，要求走完所有空格，最后到某一终点<br/>
解：backtrack + DFS 3^N 复杂度，没有更优的方法
