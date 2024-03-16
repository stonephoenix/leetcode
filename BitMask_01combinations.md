# Bit Mask == 0/1 combinations
[320. Generalized Abbreviation](https://leetcode.com/problems/generalized-abbreviation/) &nbsp;&nbsp; 对于 0/1 组合问题，bit mask 最合适不过了。不过也可用 backtrack/DFS 来做，而且考虑到有重复字符串的情况，增加 memo 可以用空间换来时间进一步减少。<br/>

[411. Minimum Unique Word Abbreviation](https://leetcode.com/problems/minimum-unique-word-abbreviation/submissions/1204623893/) &nbsp;&nbsp; 找到target最短缩写，与dictionary中单词所有缩写都不同。根据 320，不能缩写的地方为与其它单词有diff的位置，假如某位置 i 与所有单词该位置均不同，结果为 i 位不缩写，其它缩写；若 i 位与某些单词 i 位相同，则需要引入第二个不同位置，依次类推，对所有不同位置 idx 找 combination，找缩写后最短的形式。<br/>
解：既需要行方向，与每个单词找 diff， 又需要列方向，找 i 位与所有单词是否有diff，再列的各种组合，实现或之后均不同。


[2035. Partition Array Into Two Arrays to Minimize Sum Difference](https://leetcode.com/problems/partition-array-into-two-arrays-to-minimize-sum-difference/description/) &nbsp;&nbsp; 2N个数，均分两组，求两组和差值最小。<br/>
解：直接分成 N + N，左右分别遍历所有组合并求和，然后左出一个数，在右边出 N-1 个数的组合中 BS 找和最接近 sum/2 的值，以些类推。
