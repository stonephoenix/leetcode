# Manacher: m[p] = r=radius, 右半侧复用左半侧结果 [LC409](https://leetcode.com/problems/longest-palindrome/)
处理 index=p 后，对于 [p+1:p+r] 中的元素，它们各自的对称半径，镜像复用 m[p-r:p-1], 注意 __最大索引不能超过处理过的最大索引 p+r__
```Python3
idx: 012345678910
str: _b_a_b_a_d_
m:   010303  | <- right_idx = 8 处理过的索引边界
sym:   030|
m:         03  <- p=7, r=3, p+r=10 > 8 超过处理过的索引边界，不能使用镜像的3，只能用更小值1（保证索引不超过处理过的最大索引）

chars = '*' + '*'.join(s) + '*'
m = [0] * len(chars)
p = right = maxlength = maxp = 1
while p < len(chars):
    length = m[p]
    if length > 0 and p + length < right:
        p += 1
        continue
    while p + length + 1 < len(chars) and p - length - 1 >= 0 \
            and chars[p + length + 1] == chars[p - length - 1]:
        length += 1
        right = p + length
    m[p] = length
    if length > maxlength:
        maxlength = length
        maxp = p
    # print(p, length)
    for i in range(1, length + 1):
        m[p + i] = min(m[p - i], right - p - i)
    p += 1
```
