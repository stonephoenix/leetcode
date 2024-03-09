# trackback 经常用，此处记其它用法

## 记 grid 中 i 来表示一整行，j...
[51. N-Queens](https://leetcode.com/problems/n-queens/description/) &nbsp;&nbsp; 
[1001. Grid Illumination](https://leetcode.com/problems/grid-illumination/description/) &nbsp;&nbsp; 开灯亮一整行、列、对角、反对角；关灯时关指定及所有近邻共9处灯。求每次关灯前所在位置是否亮着。<br/>
解：memoi 除了记 i 行有灯，还有记有几展，用于关灯时逐一减少。memo[i] += 1, memo[j]+=1, memo[i-j]+=1, memo[i+j]+=1，注意开的时候会重复开，等一些细节。<br/>
