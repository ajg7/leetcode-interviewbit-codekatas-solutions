## 744. Find Smallest Letter Greater Than Target

```csharp
public class Solution {
    public char NextGreatestLetter(char[] letters, char target) {
        int low = 0, high = letters.Length - 1;

        while (low <= high) {
            int mid = low + (high - low) / 2;
            if (letters[mid] > target) {
                high = mid - 1;
            } else {
                low = mid + 1;
            }
        }
        return letters[Math.Max(low, high) % letters.Length];
    }
}
```
