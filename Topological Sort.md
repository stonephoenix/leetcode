# Topological Sort, 边为权重，从某一/几节点开始，对所有结点进行排序。Kahn's Algorithm: 从 indegree=0 的结点开始, reduce indegree of all neighbors, add to new_start if indegree==0

[207. Course Schedule](https://leetcode.com/problems/course-schedule/) &nbsp;&nbsp; __Kahn's Algorithm__ check cycle exists <br/>
[210. Course Schedule II](https://leetcode.com/problems/course-schedule-ii/description/) &nbsp;&nbsp; no weight <br/>
[1136. Parallel Courses](https://leetcode.com/problems/parallel-courses/description/) &nbsp;&nbsp; DFS+memo to find loop <br/>
[2050. Parallel Courses III](https://leetcode.com/problems/parallel-courses-iii/description/) &nbsp;&nbsp; with weight<br/>


[1462. Course Schedule IV](https://leetcode.com/problems/course-schedule-iv/submissions/1211661948/) &nbsp;&nbsp; queries判断多个是否存在依赖。构建 neighbor=defaultdict(list), dfs(i) + memo 存储各节点的所有子结点。<br/>
