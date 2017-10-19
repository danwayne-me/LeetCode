##Quiz#163

给定二叉树中序和后序遍历, 还原二叉树

和quiz#105类似, 用递归的方式进行构建

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
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        return buildTree(inorder, postorder, 0, inorder.length, 0, postorder.length);
    }
    
    public TreeNode buildTree(int[] inorder, int[] postorder, int inStart, int inEnd, int postStart, int postEnd) {
        if (inStart >= inEnd || postStart >= postEnd) return null;
        TreeNode node = new TreeNode(postorder[postEnd-1]);
        for (int i = inStart;i < inEnd;i++) {
            if (inorder[i] == postorder[postEnd-1]) {
                node.left = buildTree(inorder, postorder, inStart, i, postStart, postStart+i-inStart);
                node.right = buildTree(inorder, postorder, i+1, inEnd, postStart+i-inStart开下窗户呀，现在工区已经不可能开冷风啦，马上要开热风了￼, postEnd-1);
            }
        }
        return node;
    }
}
```