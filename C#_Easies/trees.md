## 938. Range Sum of BST

### Brief Explanation

    In BST left nodes are lower than the root node & right nodes are higher than the root node.
    1. After the base case, we check to see if the node is less than the low (left), if it is then, it checks its right node
    2. If that node is not less than the low, then we check to see if it is higher than the high (right), it is then, it checks its left node
    3. Finally add the results of the recursive calls and return it

```csharp
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

    In preorder traversal, first you visit the root node, then its left and then its right child.
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

## 94. Binary Tree Inorder Traversal

```csharp
public class Solution {
    public IList<int> InorderTraversal(TreeNode root) {
        IList<int> nodes = new List<int>();
        inorderHelper(nodes, root);
        return nodes;
    }

    public void inorderHelper(IList<int> nodes, TreeNode root) {
        if (root == null) return;
        inorderHelper(nodes, root.left);
        nodes.Add(root.val);
        inorderHelper(nodes, root.right);
    }
}
```

## 637. Average of Levels in Binary Tree

```csharp
public class Solution {
    public IList<double> AverageOfLevels(TreeNode root) {
        IList<double> list = new List<double>();
        Queue<TreeNode> queue = new Queue<TreeNode>();
        queue.Enqueue(root);
        while(queue.Count != 0) {
            long sum = 0, count = 0;
            Queue<TreeNode> temp = new Queue<TreeNode>();
            while (queue.Count != 0) {
                TreeNode n = queue.Dequeue();
                sum += n.val;
                count++;
                if (n.left != null) temp.Enqueue(n.left);
                if (n.right != null) temp.Enqueue(n.right);
            }
            queue = temp;
            list.Add(sum * 1.0 / count);
        }
        return list;
    }
}
```

## 872. Leaf-Similar Trees

```csharp
public class Solution {
    public bool LeafSimilar(TreeNode root1, TreeNode root2) {
        if(root1 == null && root2 == null) return true;
        if(root1 == null || root2 == null) return false;

        List<TreeNode> list1 = new List<TreeNode>();
        List<TreeNode> list2 = new List<TreeNode>();

        InOrder(root1, list1);
        InOrder(root2, list2);

        if(list1.Count != list2.Count) return false;

        for(int i = 0; i < list1.Count; i++)
        {
            if (list1[i].val != list2[i].val) return false;
        }

        return true;
    }

    private void InOrder(TreeNode root, List<TreeNode> list)
    {
        if (root != null)
        {
            InOrder(root.left,list);
            if (root.left == null && root.right == null) list.Add(root);
            InOrder(root.right,list);
        }
    }
}
```

## 108. Convert Sorted Array to Binary Search Tree

```csharp
public class Solution {
    public TreeNode SortedArrayToBST(int[] nums) {
        if(nums.Length == 0) return null;
        return getMid(nums, 0, nums.Length - 1);
    }
    public TreeNode getMid(int[] nums,int l,int r){
        if(l > r) return null;
        int mid = (l + r) / 2;
        TreeNode tree = new TreeNode(nums[mid]);
        tree.left = getMid(nums, l, mid - 1);
        tree.right = getMid(nums, mid + 1, r);
        return tree;
    }
}
```

## 144. Binary Tree Preorder Traversal

```csharp
public class Solution {
    public IList<int> PreorderTraversal(TreeNode root) {
        IList<int> nodes = new List<int>();
        PreOrder(root, nodes);
        return nodes;
    }
    private void PreOrder(TreeNode node, IList<int> nodes)
    {
        if (node == null) return;
        nodes.Add(node.val);
        PreOrder(node.left, nodes);
        PreOrder(node.right, nodes);
    }
}
```

## 145. Binary Tree Postorder Traversal

```csharp
public class Solution {
    public IList<int> PostorderTraversal(TreeNode root) {
        IList<int> nodes = new List<int>();
        PostOrder(root, nodes);
        return nodes;
    }

    public void PostOrder(TreeNode node, IList<int> nodes)
    {
        if (node == null) return;
        PostOrder(node.left, nodes);
        PostOrder(node.right, nodes);
        nodes.Add(node.val);
    }
}
```

## 653. Two Sum IV - Input is a BST

```csharp
public class Solution {
    public bool FindTarget(TreeNode root, int k)
    {
        IList<int> nodes = new List<int>();
        InOrder(root, nodes);
        int right = nodes.Count() - 1;
        int left = 0;
        while (left < right) {
            int sum = nodes[left] + nodes[right];

            if (sum == k) return true;

            if (sum > k) right--;
            else left++;
        }

        return false;
    }

    public void InOrder(TreeNode root, IList<int> nodes)
    {
        if (root == null) return;
        InOrder(root.left, nodes);
        nodes.Add(root.val);
        InOrder(root.right, nodes);
    }
}
```

## 100. Same Tree

```csharp
public class Solution {
    public bool IsSameTree(TreeNode p, TreeNode q) {
        if (p == null && q == null) return true;
        else if (p == null || q == null || p.val != q.val) return false;
        else
        {
            bool isLeftSameTree = IsSameTree(p.left , q.left);
            bool isRightSameTree = IsSameTree(p.right , q.right);
            return isLeftSameTree && isRightSameTree;
        }
    }
}
```

## 235. Lowest Common Ancestor of a Binary Search Tree

    Just walk down from the whole tree's root as long as both p and q are in the same subtree (meaning their values are both smaller or both larger than root's). This walks straight from the root to the LCA, not looking at the rest of the tree, so it's pretty much as fast as it gets.

```csharp
public class Solution {
    public TreeNode LowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (p.val < root.val && root.val > q.val) return LowestCommonAncestor(root.left, p, q);

        if (p.val > root.val && root.val < q.val) return LowestCommonAncestor(root.right, p, q);

        return root;
    }
}
```

## 543. Diameter of Binary Tree

```csharp
public class Solution {
    public int DiameterOfBinaryTree(TreeNode root) {
        int max = 0;

        int _DiameterOfBinaryTree(TreeNode root) {
            if (root == null) {
                return 0;
            }

            int left = _DiameterOfBinaryTree(root.left);
            int right = _DiameterOfBinaryTree(root.right);

            max = Math.Max(max, left + right);
            return 1 + Math.Max(left, right);
        }


        _DiameterOfBinaryTree(root);
        return max;
    }
}
```

## 606. Construct String from Binary Tree

```csharp
public class Solution {
    public string Tree2str(TreeNode root) {
        if(root == null) return "";
        string left = Tree2str(root.left);
        string right = Tree2str(root.right);

        if(left == "" && right == "") return  root.val + "";

        return root.val + "(" + left  + ")" + (right == "" ? "" : "(" + right + ")");
    }
}
```

## 257. Binary Tree Paths

```csharp
public class Solution {
    public IList<string> BinaryTreePaths(TreeNode root) {
        IList<string> list = new List<string>();
        if (root != null) SearchBT(root, "", list);
        return list;
    }

    public void SearchBT(TreeNode root, string path, IList<string> list)
    {
        if (root.left == null && root.right == null) list.Add(path + root.val);
        if (root.left != null) SearchBT(root.left, path + root.val + "->", list);
        if (root.right != null) SearchBT(root.right, path + root.val + "->", list);
    }
}
```

## 530. Minimum Absolute Difference in BST

```csharp
public class Solution {
    int minDiff = int.MaxValue;
    TreeNode prev;

    public int GetMinimumDifference(TreeNode root) {
        Inorder(root);
        return minDiff;
    }

    public void Inorder(TreeNode root)
    {
        if (root == null) return;
        Inorder(root.left);
        if (prev != null) minDiff = Math.Min(minDiff, root.val - prev.val);
        prev = root;
        Inorder(root.right);
    }
}
```
