# Binary Search: 给定区间中，查找左侧有效区间最大值（或右侧有效区间最小值），关键在于定义 is_valid()->boolean 

[1231. Divide Chocolate](https://leetcode.com/problems/divide-chocolate/description/) &nbsp;&nbsp; 一堆糖果分成 K 分，求其中糖度最小的那一份的最大值<br/>
解：糖度最小的那一份 当然可以是 min(sweetness)，然后逐渐增大，需要找到右侧边界。所以问题变成了要 搜索糖度最小那一份糖度 右边界，给定这个值的时候，当这个值太大的时候，所有的糖果无法分成 K 份，因此 is_valid 返回是否能分为 K 份。<br/>
几乎一样的题：<br/>
[1011. Capacity To Ship Packages Within D Days](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/description/)<br/>
[410. Split Array Largest Sum](https://leetcode.com/problems/split-array-largest-sum/description/)

## 一些简单上手题
[1901. Find a Peak Element II](https://leetcode.com/problems/find-a-peak-element-ii/description/) 快速找到 Max 值，DFS走较大值路径。<br/>

