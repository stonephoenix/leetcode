# Backtrack 可理解为 中序遍历 DFS 的快速剪枝，DFS 需要一层层遍历再返回，backtrack 可以根据需要一次下探多层
[320. Generalized Abbreviation](https://leetcode.com/problems/generalized-abbreviation/submissions/1204531393/) &nbsp;&nbsp; 用数字代替字母个数来对单词进行缩写，禁止两个连续数字。<br/>
解：<br/>
backtrack 思路：当前word[i] 不缩写时，append 到中间结果中，然后处理 idx=i+1；word[i] 缩写时，可以是缩写当前字母 word[i:j] = word[i:i+1]，或者 word[i:j=i+2], j=i+3..., j=n，把字母个数append到中间结果，然后处理 idx=j。
```
def generateAbbreviations(self, word: str) -> List[str]:
    ''' dfs/backtrack w/o memo
    '''
    ans = []
    n = len(word)
    def backtrack(i, cand=[]):
        if i == n:
            ans.append(''.join([str(x) for x in cand]))
            return
        # use char, proceed next
        cand.append(word[i])
        backtrack(i + 1, cand)
        cand.pop()
        # abbr if possible
        if not cand or isinstance(cand[-1], str):
            for j in range(i, n):
                cand.append(j - i + 1)
                backtrack(j + 1, cand)
                cand.pop()
    backtrack(0, [])
    return ans
```
DFS 思路，左子树:=不缩写当前结点 root.val（字母），返回上一级时，pop root.val; 右子树:=缩写当前结点（字母），需要判断父结点过来时，假如已经是缩写形式，则将缩写字母数+1，同理，返回上一级时，将缩写数-1（若为0则pop）
```
def generateAbbreviations(self, word: str) -> List[str]:
    ans = []
    n = len(word)
    def dfs(i, cand=[]):
        if i == n:
            ans.append(''.join([str(x) for x in cand]))
            return
        # left branch, use char
        cand.append(word[i])
        dfs(i + 1, cand)
        if cand:
            cand.pop()
        # right branch, use number，若上一结点已经是缩写，则缩写数+1
        if cand and isinstance(cand[-1], int):
            cand[-1] += 1
        else:
            cand.append(1)
        dfs(i + 1, cand)
        # 返回时，缩写数-1，若减为0则pop ## 这是与backtrack 稍有不同的地方，DFS 通常需要一级一级返回（这样理解上不容易出错）
        if cand:
            if isinstance(cand[-1], int) and cand[-1] > 1:
                cand[-1] -= 1
            else:
                cand.pop() #  cand=wor, return i = 2
    dfs(0, [])
    return ans
```
