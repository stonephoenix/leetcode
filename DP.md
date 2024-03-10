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
# House Robber / Paint House
[198. House Robber](https://leetcode.com/problems/house-robber/description/) &nbsp;&nbsp; 不偷连续两家。ans[i] = max(ans[i-1], nums[i] + ans[i-1]) <br/>
[213. House Robber II](https://leetcode.com/problems/house-robber-ii/description/) &nbsp;&nbsp; 不偷连续两家，房屋是一个环。DP从nums[0]开始，再算一次从nums[1]开始。
[337. House Robber III](https://leetcode.com/problems/house-robber-iii/description/) &nbsp;&nbsp; 不偷连续两家，房屋是二叉树。post order traverse， steal_root = not_steal_left + not_steal_right, not_steal_root = max(yes left + yes right, yea left + not right, not left + yes right, not left + not right), return steal_root, not_steal_root <br/>
[256. Paint House](https://leetcode.com/problems/paint-house/) &nbsp;&nbsp; 三种颜色不同cost，连续两家颜色不同，求 min tot cost。
cost[i_house][a_color] = min(cost[i-1][b], cost[i-1][c]) + cost[a]) <br/>
[265. Paint House II](https://leetcode.com/problems/paint-house-ii/description/) &nbsp;&nbsp; k种颜色不同cost，连续两家颜色不同。
cost[i_house][j_color] = min(costs[i-1][:] except costs[i-1][j])，因此需要存前一列的最小、倒数第二小值，以及最小值个数。
[276. Paint Fence](https://leetcode.com/problems/paint-fence/description/) &nbsp;&nbsp; k种颜色刷围栏，不能连续三个颜色相同，求多少种刷法。a0=k, a1=k*k, a2=(k*k*(k-1) if a2 diff from a1) + (a0 (k-1) * a1 k*k if a2 same with a1, then a0 should be diff from a1) <br/>

# Word Break / Split Array
[139. Word Break](https://leetcode.com/problems/word-break/description/)&nbsp;&nbsp; 给一个长字符串 s 和单词表，是否能将 s 分解成单词表中都有的单词。<br/>
解：从左往右遍历 i，对每一个单词，检查一下 s[i - len(word) + 1 : (i + 1)] == word and memo[i + 1 - len(word)] == 1

[140. Word Break II](https://leetcode.com/problems/word-break-ii/)&nbsp;&nbsp; 给一个长字符串 s 和单词表，找到所有将 s 分解成单词表中都有的单词 的结果。<br/>
解：可以采用139的方法，分别找出 s[0:1], s[0:2], s[0:3] ... s[0:len] 的所有分解方式。<br/>
也可以使用 backtrack + memo，假如 s 左段在单词表中，递归找 s 右边剩下的一大段。 memo中记录所有已找到的分解方式。<br/>
```
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> List[str]:
        # 递归 + memo 剪枝
        wordSet = set(wordDict)
        memo = defaultdict(list)

        def helper(s):
            if s in memo:
                return memo[s]
            if s == "":
                return []
            if s in wordSet:
                memo[s].append(s)
            for i in range(1, len(s)):
                left = s[0 : i]
                if left in wordSet:
                    right_list = helper(s[i::])
                    if right_list:
                        memo[s].extend([left + ' ' + right for right in right_list])
            return memo[s]
        helper(s)
        return memo[s]
```

[472. Concatenated Words](https://leetcode.com/problems/concatenated-words/description/)&nbsp;&nbsp; 给 list of string，字典也是它，找到能分割成至少2个单词的 单词。。<br/>
解：同上，把 prefix 也可以加到 memo 中。
```
        def helper(word, i, preparts=0):
            # start from word[i], to end, must split
            if preparts >= 2:
                memo.add(word[0:i])

            s = word[i::]
            if s in memo:
                return 2
            if s in fail:
                if s in d:
                    return 1
                else:
                    return -1

            
            '''
            # d might be very large
            for w in d:
                if len(w) < len(word) - i and w == word[i : (i + len(w))]:
                    rsplits = helper(word, i + len(w), preparts + 1)
                    if rsplits >= 1:
                        memo.add(s)
                        return 2
            '''
            # 
            for j in range(i + 1, len(word)):
                if word[i:j] in d:
                    rsplits = helper(word, j, preparts + 1)
                    if rsplits >= 1:
                        memo.add(s)
                        return 2
            fail.add(s)
            if s in d:
                return 1
            return -1
```
## Split Array 题：通常是找 min/max sum(cost)，构建转移公式实现 DP，将排列组合 K！复杂度降为 K^2。
## <span style="color:red;">还有一种看上去相近，需要找 min(每一段的 max(cost)), 需要找某单边区间最小/大值 </span>，此时问题转变为 binary search 问题，核心是构建 is_valid(). 例如 [410. Split Array Largest Sum](https://leetcode.com/problems/split-array-largest-sum/description/)
[2547. Minimum Cost to Split an Array](https://leetcode.com/problems/minimum-cost-to-split-an-array/description/) &nbsp;&nbsp; importance value (IV) = len(duplicated numbers in subarray), 找到 split 的方法，让 sum(IV) 最小。<br/>
解：split 的题通常都可以使用递归方式来解，右侧作为整体不 split，从一个 item 开始扩展更多的 item, 左侧可以 split。然后用 DP 的思路，左侧可以split的结果存在 memo 中。
''' 
minCost(num[0:n]) = minCost(
  no cut -> imp(nums[0:n]),
  cut i  -> minCost(nums[0:i]) + imp(nums[i:n])
)
#_直接计算 0:n 当然不行，使用 DP 从 j=1..n，就得到 转移公式
minCost(num[0:j]) = minCost(
  no cut -> imp(nums[0:j]),
  cut i  -> minCost(nums[0:i]) + imp(nums[i:j])
)
'''

[1547. Minimum Cost to Cut a Stick](https://leetcode.com/problems/minimum-cost-to-cut-a-stick/description/) &nbsp;&nbsp; 一根木材需要在 多处指定长度 切断，切断 cost = 当前一段长度，求总共最小 cost <br/>
解：排列组合题 k! 复杂度 通过 DP 变成 k^2. bottom up 思路：<br/>
先找两段两段的切法 boarder_cost[0:2] = len([0:2]), bc[1:3] inclusive, bc := boarder_cost <br/>
再找三段三段的切法 boarder_cost[0:3] = len([0:3]) + min(bc[0:2] + bc[2:3](=0), bc[0:1](=0) + bc[1:3])
再找四段四段的切法 boarder_cost[0:4] = len([0:4]) + min(bc[0:1] + bc[1:4], bc[0:2] + bc[2:4], bc[0:3] + bc[3:4])

# Unique Path
[62. Unique Paths](https://leetcode.com/problems/unique-paths/description/)&nbsp;&nbsp; grid 左上角至右下角，只能向右或向下，有多少种走法<br/>
解：grid[i][j] = grid[i-1][j] + grid[i][j-1]，再优化成一行DP <br/>

[63. Unique Paths II](https://leetcode.com/problems/unique-paths/description/)&nbsp;&nbsp; 62基础上增加 block cell

[980. Unique Paths III](https://leetcode.com/problems/unique-paths-iii/description/) &nbsp;&nbsp; 4个方向走，带block cell，要求走完所有空格，最后到某一终点<br/>
解：backtrack + DFS 3^N 复杂度，没有更优的方法

[2435. Paths in Matrix Whose Sum Is Divisible by K](https://leetcode.com/problems/paths-in-matrix-whose-sum-is-divisible-by-k/description/) &nbsp;&nbsp; 左上至右下之和为k倍数的路径数。<br/>
解：DFS + memo[(i,j)]={remainder: dfs path count} ; 更优的应该是分别从 左上，右下 一行一行DP，然后在中间汇合(其实只需要两行memo即可)。

__[741. Cherry Pickup](https://leetcode.com/problems/cherry-pickup/description/)__ &nbsp;&nbsp; 左上至右下，再回来，求最多摘草莓数。<br/>
解：比较难，列出所有 DFS 摘的草莓 用 bit 表示位置，然后两两进行 ｜ 操作（？）
