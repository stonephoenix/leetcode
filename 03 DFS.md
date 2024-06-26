给一个 Tree，root=0, edges 是 undirected，标准做法是先构建 defaultdict(set)，然后 DFS 时边走边删
```
neighbor = defaultdict(set)
for a, b in edges:
    neighbor[a].add(b)
    neighbor[b].add(a)

def find(root, target, depth, path=[]):
    if root == target:
        return depth
    path.append(root)
    depth += 1
    for child in neighbor[root]:
        if root in neighbor[child]:
            neighbor[child].remove(root)
        d = find(child, target, depth, path)
        if d > 0:
            return d
    path.pop()
    return -1
```
[2467. Most Profitable Path in a Tree](https://leetcode.com/problems/most-profitable-path-in-a-tree/submissions/1206529851/) &nbsp;&nbsp; DFS find，同时找中间。<br/>

__有向图判断环__：可以用BFS中的 Kahn 方法，把 indegree==0 的结点一个个删掉。也可以用 DFS + visted + cur_path 的标准解法。
```
loop = False
visted = [0] * n
cur_path = [0] * n
def dfs(i):
    nonlocal loop
    if cur_path[i]:
        loop = True
        return
    if visted[i]:
        return
    visted[i] = cur_path[i] = 1
    for child in get_child(i):
        dfs(child)
    # 注意回退时清空当前路径
    cur_path[i] = 0
[dfs(i) for i in range(n)]
```

BST 性质：
* 前序遍历时，本质是构建一个递减stack，出现大的数 large 时，最后 pop 出去的数 p 是 large 父结点，large 是 p 右结点，后面的数都大于 p。[255. Verify Preorder Sequence in Binary Search Tree](https://leetcode.com/problems/verify-preorder-sequence-in-binary-search-tree/description/) &nbsp;&nbsp; 


# Grid
[1391. Check if There is a Valid Path in a Grid](https://leetcode.com/problems/check-if-there-is-a-valid-path-in-a-grid/) &nbsp;&nbsp; grid 中有不同的道路形状（从左至右/右至左，从左拐至上方/上方拐至左方），问是否能从左上角走至右下角 <br/>
解：题简单，关键是构建状态转移时，需要保持方向定义一致，进入时以本block为准，出去时以下一block为准。<br/>

## Word Search
[79. Word Search](https://leetcode.com/problems/word-search/)&nbsp;&nbsp; 从字母grid中判断某单词是否存在 <br/>

[212. Word Search II](https://leetcode.com/problems/word-search-ii/)&nbsp;&nbsp; 从字母grid中找有几个单词 在给定单词表中 <br/>
解：DFS + Trie Tree <br/>
```
trie = dict()
for word in words:
    t = trie
    for char in word:
        if char not in t:
            t[char] = dict()
        t = t[char]
    t['eow'] = 1
```
