# BFS with bitmask or [Floyd-Warshall](https://houbb.github.io/2020/01/23/data-struct-learn-03-graph-floyd)
#### Floyd-Warshall: dist(i, j) = min(dist(i, j), dist(i, k) + dist(k, j)) for all k, 循环时，先对 k 进行循环: 相当于把 node_0 的一跳近邻形成两两互连 cluster_0（找到最近距离），若 node_k 属于 node_0 一跳近邻，则已经处理过；<br/> 若 node_k 与 node_0 的一跳近邻 node_s 相连: 若 s < k 则处理 s 的时候已经把 k 和 0 相连，然后处理 0 的时候，把 k 与0的所有一跳近邻形成两两互连; 若 s > k，则处理 s 的时候，由于 s 与 cluster_0 所有节点直连，s 会把 k 与 cluster_0 中所有点形成直连；<br/> 若 node_k 形成一个独立的 cluster_1，其中 node p 与 cluster_0 中的 s 连接，处理 s 时，由于 node s 与 cluster_0 所有节点直连，node p 也与 cluster_1 中所有节点直连，处理 s 时，p 与 cluster0 都是 s 的近邻，处理 s 后 p 与 cluster0 所有节点直连，再处理 p 时，由于 cluster 0 与 cluster 1 中所有节点均与 p 是直连，处理后 cluster0 与 cluster1 中所有点相互形成直连。
```Python3
# 为了保存ij最短路径上经过的点，最后一维增加一个数存 bitmask
for i in range(n): a[i][i][1] = 1 << i
for k in range(n):
  for i in range(n):
    for j in range(n):
      # a[i][j][0] = min(a[i][k][0] + a[k][j][0])
      if a[i][j][0] > a[i][k][0] + a[k][j][0]:
        a[i][j][0] = a[i][k][0] + a[k][j][0]
        a[i][j][1] = a[i][k][1] | a[k][j][1]
```
一些简单的：[684. Redundant Connection](https://leetcode.com/problems/redundant-connection/submissions/1208352732/) 找到最后一个多余的边，让树变成了图。可用DFS，但用 union find 更合适。
[685. Redundant Connection II](https://leetcode.com/problems/redundant-connection-ii/description/) 684中无向边变成有向边，只能用DFS来找环。

[847. Shortest Path Visiting All Nodes](https://leetcode.com/problems/shortest-path-visiting-all-nodes/editorial/) &nbsp;&nbsp; 最短路径遍历所有点（可重复经过）<br/>
解：类比 grid 取钥匙问题，相当于每个节点都有一个钥匙，求最短路径拿到所有钥匙。BFS，status = (cur_node, visted_bitmask) <br/>
还可以先找出两两之间最短距离，以及路径上经过的点，再dfs遍历所有点，当 mask 被完全染色时 提前停止。__注意：为借助DP，DFS 时一定要把当前状态，以及解决当前状态需要的答案 存下来__
```
@lru_cache(None):
def dfs(node, status):
  if status == end_status:
    return 0
  # process current node
  min_steps = sys.maxsize
  for child_node in node.children:
    min_steps = min(min_steps, dfs(new_status, child_node))
  return min_steps
```
