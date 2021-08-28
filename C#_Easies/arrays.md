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

### 1. Two Sum

```csharp
public class Solution {
    public int[] TwoSum(int[] nums, int target) {
         Dictionary<int, int> dict = new Dictionary<int, int>();

        for(int i = 0; i < nums.Length; i++)
        {
            if (dict.ContainsKey(target - nums[i])) // checks if compliment is in dict
            {
                return new int[] { dict[target - nums[i]], i };
            }
            else if (!dict.ContainsKey(nums[i])) // handles duplicates in array
            {
                dict.Add(nums[i], i);
            }
        }

        return null;
    }
}
```

```csharp
public class Solution {
    public int[] TwoSum(int[] nums, int target) {
        Dictionary<int, int> dict = new Dictionary<int, int>();

        for (int i = 0; i < nums.Length; i++) {
            int candidate = target - nums[i];
            if (dict.ContainsKey(candidate)){
                return new int[] { dict[candidate], i };
            }

            dict[nums[i]] = i;
        }
        return null;
    }
}
```
