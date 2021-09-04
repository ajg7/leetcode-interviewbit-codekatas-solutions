## 530. Minimum Absolute Difference in BST
```javascript
const getMinimumDifference = (root) => {
    const inorder = (root) => {
        if (root === null) {
            return;
        }

        inorder(root.left);

        if (prev !== null) {
            const diff = Math.abs(prev - root.val);
            minDiff = Math.min(minDiff, diff);
        }
        
        prev = root.val;

        inorder(root.right);
    }   
    
    let prev = null;
    let minDiff = Infinity;
    
    inorder(root);
    
    return minDiff;
};
```