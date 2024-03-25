# 一些技术不复杂，但题意不容易理解的stack题
[316. Remove Duplicate Letters](https://leetcode.com/problems/remove-duplicate-letters/description/) &nbsp;&nbsp; 移除重复的字母，并使得留下来的按字母序最小。<br/>
解：ca -> ca; cac -> [c]ac -> ac ; cbac -> [c]bac -> bac ; 本质上是，新的字母比stack[-1] 要小，同时未来还有和 stack[-1] 一样的字母，这个时候可以把 stack[-1] pop out。<br/>

[255. Verify Preorder Sequence in Binary Search Tree](https://leetcode.com/problems/verify-preorder-sequence-in-binary-search-tree/description/) &nbsp;&nbsp; BST 前序遍历性质：递减stack，碰到一个大的数 large 时最后 pop 出去的数 p，为全局最小值，因为 large 是 p 的右结点，后面新出来的数只能是 large 的左结点，或者右侧一片更大的数。<br/>

