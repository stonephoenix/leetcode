# min steps in Grid/Matrix
[490. The Maze](https://leetcode.com/problems/the-maze/description/) &nbsp;&nbsp; 足球滚到墙边才停， 问是否 可以从 start 到 destination <br/>
[505. The Maze II](https://leetcode.com/problems/the-maze-ii/description/) &nbsp;&nbsp; 足球滚到墙边才停，问最少滚动多少步 可以从 start 到 destination <br/>
解：BFS，min steps 这一类问题 __visted[(x, y)]__ 要把到达该点的 __steps (or min_steps) 存下来__，因为可能别的路径也到达该点，而且需要步数更少，因此不能只用一个 set 只让 BFS 过程中只经过一次。
（BFS 是一层一层展开，但不同点展开下一层时的 steps 可能是不一样的，即带权重的 graph）<br/>
其它：这个题要记录来源方向，下一次走必须走另一方向（横着来只能竖着走下一步，不能横着，横着就回去了）



