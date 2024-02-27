# [Monotonic Stack](https://leetcode.com/tag/monotonic-stack/)

[84. Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/description/) &nbsp;&nbsp; 柱状图中找最大面积 <br/>
解：先简化问题，假如是递增柱图 [1, 2, 3, 4]，需要计算 idx[0:3] (both inclusive), idx[1:3], idx[2:3], idx[3:3] 这些面积 <br/>
若增加了一个低的柱子  [1, 2, 3, 4, 2]，可以发现 值 3、4 将不起作用，需要计算 idx[0:4], idx[1:4] 这些面积, idx[2:3], idx[3:3] <br/>
本质上是，__每一个数，需要在右邻近找到 值比自己值大的区间的 右边界（边界值小于该数）__ <br/>
[1] <- 2 下一个数大于当前值，新的值为当前值的右边界 <br/>
&nbsp;&nbsp; [1 2] <- 3 下一个数继续大于最新值，大家的右边界进一步往右扩展，[1 2 3 4 。。。] <br/>
&nbsp;&nbsp; [1 2] <- 1 下一个数小于最新值，最新值的右边界找到；再看左邻数，若最新值 大于 该数，说明该数的 右边界可以进一步扩展 <br/>
&nbsp;&nbsp; [1 2] <- 0 下一个数小于最新值，最新值的右边界找到；再看左邻数，若最新值 小于 该数，说明该数的 最新值为该数的 右边界
[1] <- 0 下一个数小于当前值，右边界找到 <br/>
上面整个过程就是单调栈的过程。

