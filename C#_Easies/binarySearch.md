## 744. Find Smallest Letter Greater Than Target

```csharp
public class Solution {
    public char NextGreatestLetter(char[] letters, char target) {
        
        int left = 0;
        int right = letters.Length;
        
        while (left < right) {
            int mid = (right - left) / 2 + left;
            if (letters[mid] > target) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        
        if (left >= letters.Length) {
            return letters[0];
        } else {
            return letters[left];
        }
    }
}
```
