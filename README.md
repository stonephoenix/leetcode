# leetcode
solutions and explanations </br>
DP

## Matrix
[1074. Number of Submatrices That Sum to Target](https://leetcode.com/problems/number-of-submatrices-that-sum-to-target/)&nbsp;&nbsp;二维数字矩阵找 submatrix 的和为 target<br/>
解：presum，对每一行 i_end 都需要遍历 i_start in range(0, iend)，然后，遍历 col 时，可参照一维 presum 的方式。
O(row^2 * col)

