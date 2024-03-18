Grid min steps 代码通用模板，注意：重复访问 i, j 时，不能仅靠boolean标记，有时候需要再判断 status 才能确认是否为重复访问。例如：[1293 grid里有墙，可以敲掉 k 块墙](https://leetcode.com/problems/shortest-path-in-a-grid-with-obstacles-elimination/description/)；[296 最佳汇合点中标记已经有 k 个人汇合](https://leetcode.com/problems/best-meeting-point/description/)；[864 已经拿到了几个钥匙](https://leetcode.com/problems/shortest-path-to-get-all-keys/) <br/>
${\color{red}\textbf{扩展到图中}}$，[847 最短路径遍历所有点](https://leetcode.com/problems/shortest-path-visiting-all-nodes/description/)，status=(cur_node, visted_bitmask), 其中 visted_bitmask 可以理解成 864 中已经拿了几个钥匙（相当于每个节点都是钥匙）
```Python3
m, n = len(grid), len(grid[0])
start_status = (i, j, status)
dq = deque([[start_status, steps=0]])
visted = set([start_status])

while dq:
  (i, j, status), steps = dq.popleft()

  if i == i_end and j == j_end and status == status_end:
    return steps

  for di, dj in [[-1, 0], [1, 0], [0, -1], [0, 1]]:
    ni, nj = i + di, j + dj
    if 0 <= ni < m and 0 <= nj < n:
      news_tatus = update_status()
      if (ni, nj, new_status) not in visted:
        visted.add((ni, nj, new_status))
        dq.append([(ni, nj, new_status), steps + 1])
return -1
```
# 自定义 status , 剪枝
[773. Sliding Puzzle](https://leetcode.com/problems/sliding-puzzle/description/) &nbsp;&nbsp; 1至m*n-2填充在m*n grid中，有一个block值为0，该block可以与上下左右进行交换，求最少多少步可以让grid恢复成[[1,2,3],[4,5,0]]状态。<br/>
解：status 定义为 board 所有数字位置的状态（自定义一个hash值）。
[2304. Minimum Path Cost in a Grid](https://leetcode.com/problems/minimum-path-cost-in-a-grid/description/)  &nbsp;&nbsp; 剪枝至 length = n <br/>

# min steps in Grid/Matrix
[490. The Maze](https://leetcode.com/problems/the-maze/description/) &nbsp;&nbsp; 足球滚到墙边才停， 问是否 可以从 start 到 destination <br/>
[505. The Maze II](https://leetcode.com/problems/the-maze-ii/description/) &nbsp;&nbsp; 足球滚到墙边才停，问最少滚动多少步 可以从 start 到 destination <br/>
解：BFS，min steps 这一类问题 __visted[(x, y)]__ 要把到达该点的 __steps (or min_steps) 存下来__，因为可能别的路径也到达该点，而且需要步数更少，因此不能只用一个 set 只让 BFS 过程中只经过一次。
（BFS 是一层一层展开，但不同点展开下一层时的 steps 可能是不一样的，即带权重的 graph）<br/>
其它：这个题要记录来源方向，下一次走必须走另一方向（横着来只能竖着走下一步，不能横着，横着就回去了）<br/>

# Island
[827. Making A Large Island](https://leetcode.com/problems/making-a-large-island/description/) &nbsp;&nbsp; 允许将一个水域0转为陆地1，求最大的陆地面积 <br/>
解：每次BFS找所有陆地时，把boundary存起来，再用一个 dict 把每一个boundary cell 旁边的陆地面积存起来，下次这个 cell 又成为另外一片陆地的 boundary 时，面积累计起来。 <br/>
注意：corner case：grid 全为 0 或者 全为 1
