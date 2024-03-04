# [Monotonic Stack](https://leetcode.com/tag/monotonic-stack/) <br/>
递增 stack，能保留在栈中的数 nums[i]=v，说明右侧加进来的值都大于 v, 当 v 被 pop 出时，表示找到了第一个小于 v 的数。 <br/>
=> 性质1: 构建过程，本质上是，在右侧找到 第一个小于自己的数 <br/>
=> 性质2: 入栈 new_v 时，pop 出去的数，是大于 new_v 的连续递增序列（递减的数在之前就被 pop 出去了） <br/>
=> 最后的stack属性：两两相邻的数，左值小于等于右值，在构建中被 pop 出去的数，都是大于右值的数。 <br/>

[1762. Buildings With an Ocean View](https://leetcode.com/problems/buildings-with-an-ocean-view/submissions/1190821863/)&nbsp;&nbsp; 构建一个递减序列

[84. Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/description/) &nbsp;&nbsp; 柱状图中找最大面积 <br/>
解：先简化问题，假如是递增柱图 [1, 2, 3, 4]，需要计算 idx[0:3] (both inclusive), idx[1:3], idx[2:3], idx[3:3] 这些面积 <br/>
若增加了一个低的柱子  [1, 2, 3, 4, 2]，可以发现 值 3、4 将不起作用，需要计算 idx[0:4], idx[1:4] 这些面积, idx[2:3], idx[3:3] <br/>
本质上是，__每一个数，需要在右侧找到 第一个小于自己的数/大于自己的数的rr右边界__ <br/>
[1] <- 2 下一个数大于当前值，新的值为当前值的右边界 <br/>
&nbsp;&nbsp; [1 2] <- 3 下一个数继续大于最新值，大家的右边界进一步往右扩展，[1 2 3 4 。。。] <br/>
&nbsp;&nbsp; [1 2] <- 1 下一个数小于最新值，最新值的右边界找到；再看左邻数，若最新值 大于 该数，说明该数的 右边界可以进一步扩展 <br/>
&nbsp;&nbsp; [1 2] <- 0 下一个数小于最新值，最新值的右边界找到；再看左邻数，若最新值 小于 该数，说明该数的 最新值为该数的 右边界
[1] <- 0 下一个数小于当前值，右边界找到 <br/>
上面整个过程就是单调栈的过程。<br/>
注意：在 pop 的过程中，当前 pop 出的柱高，对应矩形的宽
heights : [1 2 2 4 3] <- 2 <br/>
idx stack:[0 1 2 _ 4] <- 5=i
stack val:[1 2 2 _ 3] <- 2 , 此时需要把 heights[4]（val=3）给 pop 出来，但 值 3 的左侧，有一个更高的 4 在之前被pop出去了，因此宽度应该使用 i - stack[-1] - 1

[85. Maximal Rectangle](https://leetcode.com/problems/maximal-rectangle/submissions/1188882670/)  &nbsp;&nbsp; 0/1 matrix 中找最大矩形 <br/>
解：沿列方向 presum，就变成问题 84 了。

[1793. Maximum Score of a Good Subarray](https://leetcode.com/problems/maximum-score-of-a-good-subarray/description/) &nbsp;&nbsp; 包含 index = k 的最大矩形面积 <br/>
解：对每一个数，找到以它为最低点的 最大矩形面积，以及左右边界。再遍历每一个数对应的左右边界，假如覆盖了 k 则有效，找所有有效的最大面积。 <br/>
左右两个方向分别 用 mono stack 找一次 next smaller。

[1944. Number of Visible People in a Queue](https://leetcode.com/problems/number-of-visible-people-in-a-queue/description/)&nbsp;&nbsp; 找 nums[i]=v 右侧值均小于 v 的连续递增序列个数 <br/>
解：考查性质2，由于是往右找被pop出去的数，因此从右往左扫描 nums

[907. Sum of Subarray Minimums](https://leetcode.com/problems/sum-of-subarray-minimums/description/)&nbsp;&nbsp; 给定 nums，求 sum(min(subarray)) for all subarrays. <br/>
eg. nums=[1,4,2], ans=sum(min(nums[0:1]), min(nums[0:2]), min(nums[0:3]), min(nums[1:2]), min(nums[1:3]), min(nums[2:3])) <br/>
解：找出以当前值为 最小值 的左右边界，再反算出组合数目。 <br/>
注意：相同的数，左边界包含并继续拓展，右边界不包含，以消除重复计算。

[2104. Sum of Subarray Ranges](https://leetcode.com/problems/sum-of-subarray-ranges/description/)&nbsp;&nbsp; 给定 nums，求 sum(max(subarray) - min(subarray)) for all subarrays. <br/>
解：==> sum(max(subarray)) - sum(min(subarray)) ==> 上一题 907

# Range Sum 问题： Binary Indexed Tree
[308. Range Sum Query 2D - Mutable](https://leetcode.com/problems/range-sum-query-2d-mutable/description/)

# Find All Next Larger Numbers 问题： Segment Tree
[2940. Find Building Where Alice and Bob Can Meet](https://leetcode.com/problems/find-building-where-alice-and-bob-can-meet/solutions/4305014/segment-tree-binary-search/)  &nbsp;&nbsp; 在 i, j 右侧找到比 nums[i], nums[j] 都大的第一个数 <br/>
解：用 mono stack 的方法，可能出现 i < j, nums[i] > nums[j] 但 nums[i] 下一个更大的数 nums[k]，位置在 j 左边 ie k < j，此时，需要继续找 nums[k] 下一个最大的数，直到位置在 j 右侧。超时。 <br/>
使用 线段树， segment tree
```
class SegTree:
    ''' 由于完全二叉树需要的空间为 2^n - 1，因此存放节点值的索引 可以从 1 开始，直到最末，方便操作。
    '''
    def __init__(self, a):
        # save max
        self.a = a
        self.v = [0] * (len(a) * 4)
        self._build(0, len(self.a) - 1, 1)

    def _build(self, left, right, idx):
        ''' left, right 是输入 a 的索引，idx 是线段树节点编号。
        '''
        if left == right:
            self.v[idx] = self.a[left]
            return
        mid = left + (right - left) // 2
        self._build(left, mid, idx * 2)
        self._build(mid + 1, right, idx * 2 + 1)
        self.v[idx] = max(self.v[idx * 2], self.v[idx * 2 + 1])
```
常规是搜索 [left, right] inclusive 中最大数的位置。 <br/>
在这题中，需要在[left, right] inclusive 区间中找到 大于 target 的最左侧的数（即先搜左边，若没有，再搜右边）
```
    def find(self, target, left, right, sg_left, sg_right, idx, debug=False):
        # 在 a[left，right] inclusive 区间中，找到最左边，最大值 > target
        if debug:
            print(sg_left, sg_right, 'idx', idx, self.v[idx], 't', target)
        if self.v[idx] <= target:
            return -1
        if sg_left == sg_right:
            if self.v[idx] <= target:
                return -1
            else:
                return sg_left
        sg_mid = sg_left + (sg_right - sg_left) // 2
        leftmost = -1
        if left <= sg_mid:
            leftmost = self.find(target, left, right, 
                                 sg_left, sg_mid, idx * 2, debug)
            if leftmost != -1:
                return leftmost
        if right > sg_mid:
            leftmost = self.find(target, left, right, 
                                 sg_mid + 1, sg_right, idx * 2 + 1, debug)
        return leftmost
```
