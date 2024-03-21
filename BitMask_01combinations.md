# Bit Mask == 0/1 combinations
__[leetcode discuss 中的解释及题集](https://leetcode.com/discuss/general-discussion/1125779/dynamic-programming-on-subsets-with-examples-explained)__ <br/>
__问题通常为：p 个槽位，分配 n(>p) 个 item，同时有 value[p][i item]，求怎么分配，总 value 最大。__ <br/>
所有组合为 C(n, p) = n * C(n-1, p-1)，第0个槽位，可以放 item_0, val_0 = value[0][0] + (p-1 个槽位放剩下 n-1 个 item), 可以放 item_1, val_1 = value[0][1] + (p-1 个槽位放剩下 n-1 个 item),..., 最后 max(val_0, val_1,..., val_n-1), 其中剩下哪些 item 可以用，使用 mask = [n 个 bit 位] 来表示即可。<br/>
__因此可以使用 top-down DP 来求解。典型题 [1879. Minimum XOR Sum of Two Arrays](https://leetcode.com/problems/minimum-xor-sum-of-two-arrays/) 两个数组一一配对使得XOR之和最小__
```Python3
def minimumXORSum(self, nums1: List[int], nums2: List[int]) -> int:
    n = len(nums1)

    @lru_cache(None)
    def dp(mask, i):
        # 第 i 个槽位，从样本中遍历可选的放过去，找最小
        # 可选样本为 mask = 011010 中 1 的位置。len(mask)==n.
        if i == n:
            return 0
        minval = sys.maxsize
        for j in range(n):
            # 只能遍历 n 来看哪个 item 还可用，也可以使用 set 来保存，但用了一个后需要有copy的操作很费时。
            if mask & (1 << j):
                val = dp(mask ^ (1 << j), i + 1) \
                        + (nums1[i] ^ nums2[j])
                minval = min(val, minval)
        return minval

    ans = dp((1 << n) - 1, 0)
    return ans
```
[698. Partition to K Equal Sum Subsets](https://leetcode.com/problems/partition-to-k-equal-sum-subsets/description/) &nbsp;&nbsp; memo + bit mask <br/>
解：还有一个不好理解的方法，avg = sum(nums) // k，从抽样一个开始，遍历所有抽样形式，memo[mask] = subsum % avg ，值必然会小于 avg，因此只有小于等于 k-2 个 subset 各自的和是 avg 的整数倍时，memo[mask=all_ones] > 0. 反过来，当 memo[mask=all_ones] = 0 时，说明必然有 k 个 subset 各自的和是 avg。<br/>
类似：[473. Matchsticks to Square](https://leetcode.com/problems/matchsticks-to-square/description/) k=4; [526. Beautiful Arrangement](https://leetcode.com/problems/beautiful-arrangement/description/) 直接backtrack；

[320. Generalized Abbreviation](https://leetcode.com/problems/generalized-abbreviation/) &nbsp;&nbsp; 对于 0/1 组合问题，bit mask 加一些逻辑。也可用 backtrack/DFS 来做，而且考虑到有重复字符串的情况，增加 memo 可以用空间换来时间进一步减少。<br/>

[411. Minimum Unique Word Abbreviation](https://leetcode.com/problems/minimum-unique-word-abbreviation/submissions/1204623893/) &nbsp;&nbsp; 找到target最短缩写，与dictionary中单词所有缩写都不同。根据 320，不能缩写的地方为与其它单词有diff的位置，假如某位置 i 与所有单词该位置均不同，结果为 i 位不缩写，其它缩写；若 i 位与某些单词 i 位相同，则需要引入第二个不同位置，依次类推，对所有不同位置 idx 找 combination，找缩写后最短的形式。<br/>
解：既需要行方向，与每个单词找 diff， 又需要列方向，找 i 位与所有单词是否有diff，再列的各种组合，实现或之后均不同。

[2035. Partition Array Into Two Arrays to Minimize Sum Difference](https://leetcode.com/problems/partition-array-into-two-arrays-to-minimize-sum-difference/description/) &nbsp;&nbsp; 2N个数，均分两组，求两组和差值最小。<br/>
解：直接分成 N + N，左右分别遍历所有组合并求和，然后左出一个数，在右边出 N-1 个数的组合中 BS 找和最接近 sum/2 的值，以些类推。

[847. Shortest Path Visiting All Nodes](https://leetcode.com/problems/shortest-path-visiting-all-nodes/description/) &nbsp;&nbsp; 最短步数遍历图中所有点。<br/>
解：可以用BFS做, status=(cur_node, visted_node_bitmask), memo[status]=steps for status to reach end. 还可以先用 Floyd-Warshall 方法找到所有 ij pair 之间的最短距离，然后DFS遍历所有点，bitmask 全为1时提前结束。<br/>

[1655. Distribute Repeating Integers](https://leetcode.com/problems/distribute-repeating-integers/description/) &nbsp;&nbsp; 先做小组合，然后再去 fit, 类似于 847。__TODO__ <br/>
