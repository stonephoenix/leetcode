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
