# 在窗口内进行计数，有时有次滑窗不行，可以多次（常数次）滑窗操作；<br/> 找最大/最小长度，binary search 是首选
[159. Longest Substring with At Most Two Distinct Characters](https://leetcode.com/problems/longest-substring-with-at-most-two-distinct-characters/description/) 注意distinct个数更新。<br/>
[395. Longest Substring with At Least K Repeating Characters](https://leetcode.com/problems/longest-substring-with-at-least-k-repeating-characters/editorial/) 最长子串，里面每个字母出现 k 次及以上<br/>
解：次数 k 次以下的为 split point，采用 devide-conquer 容易想到。<br/>
但直觉上可以用滑动窗口的方法，困难点是不好判断左侧移动时机，左侧移动时计数会减少，从而消减个数不够的字母，但我们不知道哪个字母未来会不够，也就是说，不确定窗口内 __应该包括哪几个字母__ 。
但退一步，最终答案中字母种类是有限的(P个，最多为字符串整体中不同字母个数），虽然不知道是哪几个，但我们可以 __先约束有p个不同的字母，然后遍历 p = 1,2,.. P__ 
使用这个约束条件对滑动窗口进行操作，最多只需要 26 次滑窗遍历s。<br/>

[1062. Longest Repeating Substring](https://leetcode.com/problems/longest-repeating-substring/description/) __Longest__ binary search，然后就是滑窗多项式 hash 优化。<br/>

