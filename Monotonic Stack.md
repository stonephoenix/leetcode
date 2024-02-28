# [Monotonic Stack](https://leetcode.com/tag/monotonic-stack/) <br/>
构建过程，本质上是，在右侧找到 第一个小于自己的数 <br/>
最后的stack属性：两两相邻的数，左值小于等于右值，在构建中被 pop 出去的数，都是大于右值的数。 <br/>

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

[85. Maximal Rectangle](https://leetcode.com/problems/maximal-rectangle/submissions/1188882670/)  &nbsp;&nbsp; 0/1 matrix 中找最大矩形<br/>
解：沿列方向 presum，就变成问题 84 了。

# Range Sum 问题： Binary Indexed Tree
[308. Range Sum Query 2D - Mutable](https://leetcode.com/problems/range-sum-query-2d-mutable/description/)
