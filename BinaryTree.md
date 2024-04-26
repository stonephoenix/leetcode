
# Binary Tree
```Python3
def lca(root, a, b):
  if not root: return root
  if root.val == a or root.val == b: return root
  left = lca(root.left, a, b)
  right = lca(root.right, a, b)
  if left and right: return root
  return left if left else right
```

# Binary Search Tree
[1382. Balance a Binary Search Tree](https://leetcode.com/problems/balance-a-binary-search-tree/description/) &nbsp;&nbsp; 平衡二叉树<br/>
解：__通用解法较难，需要回顾一下__ <br/>
inorder traverse 将树变成 list，然后取中点做为root，并递归左侧，右侧部分。<br/>
[One-Time Binary Search Tree Balancing: The Day/Stout/Warren (DSW) Algorithm, 2002](https://web.archive.org/web/20220406184919/https://sci-hub.hkvisa.net/10.1145/820127.820173)<br/>
[Tree Rebalancing in Optimal Time and Space, 1986](http://web.eecs.umich.edu/~qstout/pap/CACM86.pdf) This is the best one to read.<br/>
[Balancing a Binary Tree, Algorithms Supplement, The Computer Journal, Volume 19, Issue 4, 1976, Pages 360–363](https://academic.oup.com/comjnl/article/19/4/360/326682)<br/>

[230. Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/description/) &nbsp;&nbsp; 中序遍历即从小到大计数。fllowup，若树经常有增删变动，并再次找第k小的值。<br/>
解：一个方法是改变树结构，记录当前点所有子结点数量。O(N)空间复杂度，同时每次查询平均O(H=logN)复杂度。<br/>
更优方法是用 stack 记录当前结点路径:<br/>
若减少了一个小于Kth的数，查找较小值: 当前节点左子树最右节点，若无左子树，回溯祖先路径上第一个右子树的父节点<br/>
若增加了一个小于Kth的数，查找较大值: 当前节点右子树最左节点，若无右子树，回溯祖先路径上第一个左子树的父节点<br/>
```
```

一些简单题：[333. Largest BST Subtree](https://leetcode.com/problems/largest-bst-subtree/description/) 返回 min, max, cnt 即可。
