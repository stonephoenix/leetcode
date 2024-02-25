# Grid
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
