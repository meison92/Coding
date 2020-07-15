# [LeetCode236.二叉树的最近公共祖先](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/)
## 题目描述
给定一个二叉树, 找到该树中两个指定节点的最近公共祖先。

最近公共祖先的定义为：“对于有根树 `T` 的两个结点 `p`、`q`，最近公共祖先表示为一个结点 `x`，满足 `x` 是 `p`、`q` 的祖先且 `x` 的深度尽可能大（一个节点也可以是它自己的祖先）。”

例如，给定如下二叉树:  `root = [3,5,1,6,2,0,8,null,null,7,4]`

![](https://picgp.oss-cn-beijing.aliyuncs.com/img/20200714175105.png)

### 示例
```
输入: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
输出: 3
解释: 节点 5 和节点 1 的最近公共祖先是节点 3。
```
```
输入: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
输出: 5
解释: 节点 5 和节点 4 的最近公共祖先是节点 5。因为根据定义最近公共祖先节点可以为节点本身。
```
### 注意
- 所有节点的值都是唯一的。
- `p`、`q` 为不同节点且均存在于给定的二叉树中。

## 题解
### 解法
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        List<TreeNode> listP=new ArrayList<>();
        List<TreeNode> listQ=new ArrayList<>();
        helper(root,p,listP);
        helper(root,q,listQ);
        for(TreeNode tempP:listP){
            for(TreeNode tempQ:listQ){
                if(tempP==tempQ){
                    return tempP;
                }
            }
        }
        return null;
    }
    public boolean helper(TreeNode root,TreeNode temp,List<TreeNode> list){
        if(root==null){
            return false;
        }
        if(root==temp){
            list.add(root);
            return true;
        }
        if(helper(root.left,temp,list)||helper(root.right,temp,list)){
            list.add(root);
            return true;
        }
        return false;
    }
}
```






