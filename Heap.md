
[1642. Furthest Building You Can Reach](https://leetcode.com/problems/furthest-building-you-can-reach/submissions/1192938593/) &nbsp;&nbsp; 
一维 nums 从左往右一步一步走，等高或者从高往低无cost，从低往高需要消费 一个 ladder 或者 height diff 个 bricks，给定 a 个 ladders, b 个 bricks，求最远能走到哪里。<br/>
解：至少能消耗 a 个 ladders，若还有 从低往高 的 diff 时，将最小的 diff 使用 bricks，问题变成了 fixed size heap。
