## Binary Tree Inorder Traversal
### Problem Statement
Given the root of a binary tree, return the inorder traversal of its nodes' values.Example 1:Input:root = [1,null,2,3]Output:[1,3,2]Explanation:Example 2:Input:root = [1,2,3,4,5,null,8,null,null,6,7,9]Output:[4,2,6,5,7,1,3,9,8]Explanation:Example 3:Input:root = []Output:[]Example 4:Input:root = [1]Output:[1]Constraints:The number of nodes in the tree is in the range [0, 100].-100 <= Node.val <= 100Follow up: Recursive solution is trivial, could you do it iteratively?
### Solution
```csharp
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int val=0, TreeNode left=null, TreeNode right=null) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
public class Solution {
    public IList<int> InorderTraversal(TreeNode root) {
        IList<int> visited = new List<int>();
        InOrderTraversal(root, visited);
        return visited;
    }

    public void InOrderTraversal(TreeNode node, IList<int> visited)
    {
        if (node is null)
            return;
        
        //traverse left
        InOrderTraversal(node.left, visited);

        //add node
        visited.Add(node.val);

        //traverse right
        InOrderTraversal(node.right, visited);
    }
}
```
### Notes
