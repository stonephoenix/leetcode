# 找到 subset 和/均值/最大小值 满足一些要求，<br/> 只要求返回boolean时，最常用的是一边找一边cache，假如 sum 不大时，mark[i][sum]=True，注意更新时 从大到小 更新，否则数据被污染；<br/>若需要返回值，通常需要用 bitmask 遍历所有组合，为减少复杂度，先分左右两半。<br/>注意另一种 split array，通常用DP即可（array中插挡板）
```Python3
@lru_cache(None)
def find(target, k, i):
  # 处理 nums[i]，还需要找 k 个数
  if k == 0:
    return target == 0
  if target < 0 or k + i > len(nums):
    return False
  return find(nums, target, k, i + 1) or find(nums, target - nums[i], k - 1, i + 1)
```

[805. Split Array With Same Average](https://leetcode.com/problems/split-array-with-same-average/description/) &nbsp;&nbsp; subset 均值 与全局均值相同。<br/>
解：直接用上面 cache 方法即可。

[446. Arithmetic Slices II - Subsequence](https://leetcode.com/problems/arithmetic-slices-ii-subsequence/) &nbsp;&nbsp; 三个及以上等差数列的个数。不难，就是啰嗦一些。<br/>

[2305. Fair Distribution of Cookies](https://leetcode.com/problems/fair-distribution-of-cookies/description/) &nbsp;&nbsp; 分配给 K 个桶，求所有桶最大值的下限。backtrack + 简单剪枝（不要多想）<br/>


[1049. Last Stone Weight II](https://leetcode.com/problems/last-stone-weight-ii/description/) &nbsp;&nbsp; subset 和最接近总和一半，mark[i][sum]=True，注意更新时 从大到小 更新。<br/>



[956. Tallest Billboard](https://leetcode.com/problems/tallest-billboard/description/) &nbsp;&nbsp; 找两个不相交的 subset 它们和相同。<br/>
解：注意不是找一个subset的组合问题，因此不能先backtrack找一个subset，加上mask，再backtrack找另外一个subset，会有很多重复判断。<br/>
直接遍历所有 <rod_left_list, rod_right_list> 的组合，为减少复杂度，先将array分成左右两半。为快速找到 sum( array_left: rod_left_list) + sum( array_right: rod_left_list) == sum(array_left|right: rod_right_list), 注意到是一个 two sum equal 问题，因此可以使用 diff 的技巧：计算 diff = sum(rod_left) - sum(rod_right), 左右两半array中 diff 为负数时即为结果。
