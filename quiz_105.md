##Quiz#105

给定一个不含重复元素的二叉树的前序遍历和中序遍历, 还原该二叉树

* 递归解: 

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
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        return buildTree(preorder, inorder, 0, preorder.length, 0, inorder.length);
    }
    
    public TreeNode buildTree(int[] preorder, int[] inorder, int preStart, int preEnd, int inStart, int inEnd) {
        if (preStart >= preEnd || inStart >= inEnd) return null;
        TreeNode node = new TreeNode(preorder[preStart]);
        for (int i = inStart;i < inEnd;i++) {
            if (inorder[i] == preorder[preStart]) {
                node.left = buildTree(preorder, inorder, preStart+1, preStart+1+i-inStart, inStart, i);
                node.right = buildTree(preorder, inorder, preStart+1+i-inStart, preEnd, i+1, inEnd);
            }
        }
        return node;
    }
}
```