# 列表中插档板，通常是 memo[i][j] = sum(nums[i:(j+1)])

[548. Split Array with Equal Sum](https://leetcode.com/problems/split-array-with-equal-sum/description/) &nbsp;&nbsp; memo[i][j] = sum(nums[i:(j+1)])

## 通常是找 min/max sum(cost)，构建转移公式实现 DP，将排列组合 K！复杂度降为 K^2。
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
