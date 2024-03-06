
[3010. Divide an Array Into Subarrays With Minimum Cost I](https://leetcode.com/problems/divide-an-array-into-subarrays-with-minimum-cost-i/description/) &nbsp;&nbsp; <br/> find min K
解: 构建容量为 K 的大顶堆，push 一个数，再把最大的 pop 出去。

[3013. Divide an Array Into Subarrays With Minimum Cost II](https://leetcode.com/problems/divide-an-array-into-subarrays-with-minimum-cost-ii/description/) &nbsp;&nbsp; 滑动窗口中 find min K <br/> 
解：__from sortedcontainers import SortedList__

[1642. Furthest Building You Can Reach](https://leetcode.com/problems/furthest-building-you-can-reach/submissions/1192938593/) &nbsp;&nbsp; 
一维 nums 从左往右一步一步走，等高或者从高往低无cost，从低往高需要消费 一个 ladder 或者 height diff 个 bricks，给定 a 个 ladders, b 个 bricks，求最远能走到哪里。<br/>
解：至少能消耗 a 个 ladders，若还有 从低往高 的 diff 时，将最小的 diff 使用 bricks，问题变成了 fixed size heap。

[871. Minimum Number of Refueling Stops](https://leetcode.com/problems/minimum-number-of-refueling-stops/description/)&nbsp;&nbsp; 给初始油量，以及加油站 位置 及 油量 列表，求最少加几次油到目标点。<br/>
解：在能到达的范围内，先去油量最大的加油站。 <br/>
```
a = SortedList([1,2,3,3,3,4,5,6,4,4,4,3,2,7])
a.remove(4)
a.add(6)
#* a=SortedList([1, 2, 2, 3, 3, 3, 3, 4, 4, 4, 5, 6, 6, 7])
a.bisect(3), a.bisect_left(3), a.bisect_right(3), a.bisect_right(7)
#* (7, 3, 7, 14)
```
