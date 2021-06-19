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

## 700. Search in a Binary Search Tree

### Brief Explanation

    If the root is null, then return the node (root)
    if the root's value is equal to the value then return the node (which contains its left and right subtrees);
    If the val is less than the root's val, then go to the left side
    If the val is more than the root's val, then go to the right side
    If we make it all the way and haven't found the val node, then just return null

    * Remember this property root.left < root < root.right

```csharp
public class Solution {
    public TreeNode SearchBST(TreeNode root, int val) {
        if (root == null) return root;
        if (root.val == val) return root;
        else if (root.val > val) return SearchBST(root.left, val);
        else if (root.val < val) return SearchBST(root.right, val);
        return null;
    }
}
```

## 1022. Sum of Root To Leaf Binary Numbers

### Brief Explanation

    This is a Depth-First Search Solution
    We need make a path from root to leaf, and convert the resulting binary into an integer
    We do this by multipling the val by 2, adding the root's val, and then assigning the result into val
        Therefore val will transform into the int
    If both the left and right are equal then just the val, else run dfs again on both the left and right

```csharp
public class Solution {
    public int SumRootToLeaf(TreeNode root) {
        return dfs(root, 0);
    }

    public int dfs(TreeNode root, int val) {
        if (root == null) return 0;
        val = val * 2 + root.val;
        return root.left == root.right ? val : dfs(root.left, val) + dfs(root.right, val);
    }
}
```

## 559. Maximum Depth of N-ary Tree

```csharp
public class Solution {
    public int MaxDepth(Node root) {
        if (root == null) return 0;
        return MaxDepthFunc(root);
    }

    public int MaxDepthFunc(Node root, int max = 1, int level = 1)
    {
        max = Math.Max(max, level);

        foreach (Node node in root.children){
            max = Math.Max(MaxDepthFunc(node, max, level + 1), max);
        }
        return max;
    }
}
```

## 104. Maximum Depth of Binary Tree

```csharp
public class Solution {
    public int MaxDepth(TreeNode root) {
        int left, right, result;
        if (root == null) return 0;
        left = MaxDepth(root.left) + 1;
        right = MaxDepth(root.right) + 1;
        result = Math.Max(left, right);
        return result;
    }
}
```

## 226. Invert Binary Tree

```csharp
public class Solution {
    public TreeNode InvertTree(TreeNode root) {
        if (root == null) return null;

        TreeNode left = root.left;
        TreeNode right = root.right;
        root.right = this.InvertTree(left);
        root.left = this.InvertTree(right);

        return root;
    }
}
```

## 965. Univalued Binary Tree

```csharp
public class Solution {
    public bool IsUnivalTree(TreeNode root) {
        return search(root, root.val);
    }

    public bool search(TreeNode root, int val) {
        if (root == null) return true;

        if (root.val == val) {
            return search(root.left, val) && search(root.right, val);
        } else return false;
    }
}
```
