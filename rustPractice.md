## Rust

### 121. Best Time to Buy and Sell Stock

```rust
use std::cmp::min;
use std::cmp::max;

impl Solution {
    pub fn max_profit(prices: Vec<i32>) -> i32 {
        if (prices.len() < 2) {
            return 0;
        }

        let mut maxProfit: i32 = std::i32::MIN;
        let mut minPrice: i32 = prices[0];

        for price in prices {
            maxProfit = max(maxProfit, price - minPrice);
            minPrice = min(minPrice, price);
        }
        maxProfit as i32
    }

}
```

### 70. Climbing Stairs

#### Fibonacci Number Solution

```rust
impl Solution {
    pub fn climb_stairs(n: i32) -> i32 {
        if (n == 1) {
            return 1;
        }
        let mut first: i32 = 1;
        let mut second: i32 = 2;
        let mut count: i32 = 3;
        while (count <= n) {
            let third: i32 = first + second;
            first = second;
            second = third;
            count += 1;
        }
        second
    }
}
```

### 136. Single Number

```rust
impl Solution {
    pub fn single_number(nums: Vec<i32>) -> i32 {
        let mut singleNumber: i32 = 0;
        for num in nums {
            singleNumber ^= num;
        }

        singleNumber
    }
}
```

### 448. Find All Numbers Disappeared in an Array

```rust
use std::collections::HashSet;

impl Solution {
    pub fn find_disappeared_numbers(nums: Vec<i32>) -> Vec<i32> {
        let mut result: Vec<i32> = Vec::new();
        let mut numbers: HashSet<i32> = HashSet::new();
        let mut counter: i32 = 1;
        let length: usize = nums.len();
        for num in nums {
            numbers.insert(num);
        }
        while counter <= length as i32 {
            if !numbers.contains(&counter) {
                result.push(counter);
            }
            counter += 1;
        }
        result
    }
}
```

### 268. Missing Number

```rust
impl Solution {
    pub fn missing_number(nums: Vec<i32>) -> i32 {
        let mut missing_number: i32 = nums.len() as i32;
        let mut counter: i32 = 0;
        for num in nums {
            missing_number ^= counter ^ num;
            counter += 1;
        }
        missing_number
    }
}

#[test]

fn test() {
    assert_eq!(Solution::missing_number(vec![3, 0, 1]), 2);
}
```

### 217. Contains Duplicate

```rust
use std::collections::HashSet;

impl Solution {
    pub fn contains_duplicate(nums: Vec<i32>) -> bool {
        let mut numbers = HashSet::<i32>::new();
        for number in nums {
            if !numbers.contains(&number) {
                numbers.insert(number);
            } else {
                return true;
            }
        }
        return false;
    }
}

#[test]
fn test() {
    let nums = vec![1, 2, 3, 1];
    assert_eq!(Solution::contains_duplicate(nums), true);
}
```
