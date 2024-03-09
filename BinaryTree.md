
# Binary Tree

# Binary Search Tree
[1382. Balance a Binary Search Tree](https://leetcode.com/problems/balance-a-binary-search-tree/description/) &nbsp;&nbsp; 平衡二叉树<br/>
解：__通用解法较难，需要回顾一下__ <br/>
inorder traverse 将树变成 list，然后取中点做为root，并递归左侧，右侧部分。<br/>
[One-Time Binary Search Tree Balancing: The Day/Stout/Warren (DSW) Algorithm, 2002](https://web.archive.org/web/20220406184919/https://sci-hub.hkvisa.net/10.1145/820127.820173)<br/>
[Tree Rebalancing in Optimal Time and Space, 1986](http://web.eecs.umich.edu/~qstout/pap/CACM86.pdf) This is the best one to read.<br/>
[Balancing a Binary Tree, Algorithms Supplement, The Computer Journal, Volume 19, Issue 4, 1976, Pages 360–363](https://academic.oup.com/comjnl/article/19/4/360/326682)<br/>
