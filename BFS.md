# min steps in Grid/Matrix
[490. The Maze](https://leetcode.com/problems/the-maze/description/) &nbsp;&nbsp; 足球滚到墙边才停， 问是否 可以从 start 到 destination <br/>
[505. The Maze II](https://leetcode.com/problems/the-maze-ii/description/) &nbsp;&nbsp; 足球滚到墙边才停，问最少滚动多少步 可以从 start 到 destination <br/>
解：BFS，min steps 这一类问题 __visted[(x, y)]__ 要把到达该点的 __steps (or min_steps) 存下来__，因为可能别的路径也到达该点，而且需要步数更少，因此不能只用一个 set 只让 BFS 过程中只经过一次。
（BFS 是一层一层展开，但不同点展开下一层时的 steps 可能是不一样的，即带权重的 graph）<br/>
其它：这个题要记录来源方向，下一次走必须走另一方向（横着来只能竖着走下一步，不能横着，横着就回去了）


# Island
[827. Making A Large Island](https://leetcode.com/problems/making-a-large-island/description/) &nbsp;&nbsp; 允许将一个水域0转为陆地1，求最大的陆地面积 <br/>
解：每次BFS找所有陆地时，把boundary存起来，再用一个 dict 把每一个boundary cell 旁边的陆地面积存起来，下次这个 cell 又成为另外一片陆地的 boundary 时，面积累计起来。 <br/>
注意：corner case：grid 全为 0 或者 全为 1