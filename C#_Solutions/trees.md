## 938. Range Sum of BST

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
    public int RangeSumBST(TreeNode root, int low, int high) {
        if (root == null) return 0;
        if (root.val < low) return RangeSumBST(root.right, low, high);
        if (root.val > high) return RangeSumBST(root.left, low, high);
        return root.val + RangeSumBST(root.left, low, high) + RangeSumBST(root.right, low, high);
    }
}
```

## 617. Merge Two Binary Trees

```csharp
public class Solution {
    public TreeNode MergeTrees(TreeNode root1, TreeNode root2) {
        if (root1 == null) return root2;
        if (root2 == null) return root1;
        root1.val  += root2.val;
        root1.left = MergeTrees(root1.left, root2.left);
        root1.right = MergeTrees(root1.right, root2.right);
        return root1;
    }
}
```

## 897. Increasing Order Search Tree

```csharp
public class Solution {
    public TreeNode IncreasingBST(TreeNode root) {
        List<int> list = new List<int>();
        inorder(root, list);
        TreeNode result = new TreeNode(list[0]);
        TreeNode ans = result;
        for (int i = 1; i < list.Count(); i++) {
            ans.right = new TreeNode(list[i]);
            ans = ans.right;
        }
        return result;
    }

    private void inorder(TreeNode node, List<int> list) {
        if (node == null) return;
        inorder(node.left, list);
        list.Add(node.val);
        inorder(node.right, list);
    }
}
```

589. N-ary Tree Preorder Traversal

```csharp
public class Solution {
    public IList<int> Preorder(Node root) {
        IList<int> nodes = new List<int>();
        preOrderWalk(root, nodes);
        return nodes;
    }

    public void preOrderWalk(Node root, IList<int> nodes) {
        if (root == null) return;
        nodes.Add(root.val);
        foreach(Node node in root.children) {
            preOrderWalk(node, nodes);
        }
    }
}
```
