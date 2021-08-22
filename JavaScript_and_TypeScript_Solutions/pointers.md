## Pointers

### 844. Backspace String Compare

```javascript
const backspaceCompare = (S, T) => {
	const check = string => {
		const stack = [];
		for (const s of string) {
			if (s !== "#") stack.push(s);
			else if (stack.length !== 0) stack.pop();
		}
		return stack.join("");
	};
	return check(S) === check(T);
};
```

### 977. Squares of a Sorted Array

```csharp
public class Solution {
    public int[] SortedSquares(int[] nums) {
        int[] result = new int[nums.Length];
        
        int writeIndex = nums.Length - 1;
        
        int left = 0;
        int right = nums.Length - 1;
        
        while (left <= right) {
            int leftSquared = (int) Math.Pow(nums[left], 2);   
            int rightSquared = (int) Math.Pow(nums[right], 2);
            
            if (leftSquared > rightSquared) {
                result[writeIndex] = leftSquared;
                left += 1;
            } else {
                result[writeIndex] = rightSquared;
                right -= 1;
            }
            writeIndex -= 1;
        }
        
        return result;
    }
}
```
