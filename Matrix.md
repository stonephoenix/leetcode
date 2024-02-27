# 简单但需要思路清晰 &nbsp; 小心处理边界

[59. Spiral Matrix II](https://leetcode.com/problems/spiral-matrix-ii/submissions/1187893580/) &nbsp;&nbsp; 顺时针填入二维数组 <br/>
[2326. Spiral Matrix IV](https://leetcode.com/problems/spiral-matrix-iv/submissions/1187990393/) &nbsp;&nbsp; 顺时针填入二维数组，值来源于 linked list <br/>
[54. Spiral Matrix](https://leetcode.com/problems/spiral-matrix/submissions/1187877133/) &nbsp;&nbsp; 顺时针遍历二维数组 <br/>
解：不讨论 59 题中可以改写matrix的简单方法 <br/>
分别记录每个方向的边界，在当前方向上一直走，__while 中先判断下一步是否可以走，再走，可以简化很多边界操作__
```
while is_valid(x + dx):
  x += dx
  process_new_x(x)
```
[885. Spiral Matrix III](https://leetcode.com/problems/spiral-matrix-iii/submissions/1187965910/) &nbsp;&nbsp; 
![image](https://github.com/stonephoenix/leetcode/assets/11725857/a4e48d74-78da-40ba-97c0-371e79f0d744)

解：假如下一步已经填了数，则不填，但把坐标移到空位，或者边界； <br/>
此时位置上假如是空值，则填数，同时判断下一个方向，若可以填数/或者在边界外，则停止填数；若位置上仍有数，不操作，使用下一个方向。

