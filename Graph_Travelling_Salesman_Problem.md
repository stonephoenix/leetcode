# BFS with bitmask or [Floyd-Warshall](https://houbb.github.io/2020/01/23/data-struct-learn-03-graph-floyd)
一些简单的：[684. Redundant Connection](https://leetcode.com/problems/redundant-connection/submissions/1208352732/) 找到最后一个多余的边，让树变成了图。可用DFS，但用 union find 更合适。
[685. Redundant Connection II](https://leetcode.com/problems/redundant-connection-ii/description/) 684中无向边变成有向边，只能用DFS来找环。

[847. Shortest Path Visiting All Nodes](https://leetcode.com/problems/shortest-path-visiting-all-nodes/editorial/) &nbsp;&nbsp; 最短路径遍历所有点（可重复经过）<br/>
解：类比 grid 取钥匙问题，相当于每个节点都有一个钥匙，求最短路径拿到所有钥匙。BFS，status = (cur_node, visted_bitmask) <br/>
