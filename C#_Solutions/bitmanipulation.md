## 268. Missing Number

```csharp
public class Solution {
    public int MissingNumber(int[] nums) {
        int res = 0;
        foreach (int num in nums) {
            res ^= num;
        }
        
        for(int i = 0; i < nums.Length + 1; i++) {
            res ^= i;
        }
    return res;
    }
}
```