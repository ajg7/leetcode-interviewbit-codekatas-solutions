### 217. Contains Duplicate

```csharp
using System;

public class Solution {
    public bool ContainsDuplicate(int[] nums) {
        HashSet<int> numberSet = new HashSet<int>(nums);
        return numberSet.Count != nums.Length;
    }
}
```
