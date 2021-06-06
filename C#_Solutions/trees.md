## 938. Range Sum of BST

### Brief Explanation

    In BST left nodes are lower than the root node & right nodes are higher than the root node.
    1. After the base case, we check to see if the node is less than the low (left), if it is then, it checks its right node
    2. If that node is not less than the low, then we check to see if it is higher than the high (right), it is then, it checks its left node
    3. Finally add the results of the recursive calls and return it

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

### Brief Explanation
    First we see if the nodes of both trees is null, if it is then just return the one that has a value.
    However if they both have a value, then we need to add both of those and assign that sum to root1.val (root1 is going to be our new tree)
    Traverse down the lefts of both trees
    Then Traverse down the rights of both trees
    Return root1

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

### Brief Explanation

    Recursively call inorder with tail being the next node in the inorder
    If the root is null then we return the tail directly
    By recursively calling the root.left, we are changing the left subtree into the linked list + current node
    By recursively calling the root.right, we are chaging the right subtree into the linked list + tail
    The result is the linked list with right child being the next node, which is why we set the left to null
    Result will be inorder(root.left) -> root -> inorder(root.right)

```csharp
public class Solution {
    public TreeNode IncreasingBST(TreeNode root) {
        return inorder(root, null);
    }
    
    public TreeNode inorder(TreeNode root, TreeNode tail) {
        if (root == null) return tail;
        TreeNode result = inorder(root.left, root);
        root.left = null;
        root.right = inorder(root.right, tail);
        return result;
    }
}
```

## 589. N-ary Tree Preorder Traversal

### Brief Explanation

    In preorder traversal, first you visit the node, then its left and then its right child.
    We first check the top node, then recursively move to the left, check it out then move the left
    Check it out, then go back up and check the previous right node, check it, then back up so on and so forth

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

## 590. N-ary Tree Postorder Traversal

```csharp
public class Solution {
    public IList<int> Postorder(Node root) {
        IList<int> nodes = new List<int>();
        if (root == null) return nodes;
        postorderWalk(root, nodes);
        nodes.Add(root.val);
        return nodes;
    }
    
    public void postorderWalk(Node root, IList<int> nodes) {
        if (root == null) return;
        foreach (Node node in root.children) {
            postorderWalk(node, nodes);
            nodes.Add(node.val);
        }
    }
}
```
