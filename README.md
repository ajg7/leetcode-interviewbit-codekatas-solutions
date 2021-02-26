My solutions for leetcode, interviewbit & codekatas. Languages used: TypeScript, JavaScript, & Rust

# Leetcode

## Graphs

### 997. Find the Town Judge

```javascript
const findJudge = (N, trust) => {
	const map = {};

	for (const [person1, person2] of trust) {
		if (!map[person1]) map[person1] = { in: 0, out: 0 };
		if (!map[person2]) map[person2] = { in: 0, out: 0 };

		map[person1].out++;
		map[person2].in++;
	}

	for (const [person, degrees] of Object.entries(map)) {
		if (degrees.in === N - 1 && degrees.out === 0) {
			return +person;
		}
	}

	return -1;
};
```

## Dynamic Programming

### 303. Range Sum Query - Immutable

```javascript

```

### 53. Maximum Subarray

#### Kadane's Alogrithm

```typescript
const maxSubArray = (nums: number[]): number => {
	let maxSum: number = nums[0];

	for (let i = 0; i < nums.length; i++) {
		if (nums[i - 1] > 0) {
			nums[i] += nums[i - 1];
		}
		maxSum = Math.max(nums[i], maxSum);
	}

	return maxSum;
};
```

### 121. Best Time to Buy and Sell Stock

```typescript
const maxProfit = (prices: number[]): number => {
	if (prices.length < 2) return 0;

	let maxProfit: number = -Infinity;
	let minPrice: number = prices[0];
	for (const price of prices) {
		maxProfit = Math.max(maxProfit, price - minPrice);
		minPrice = Math.min(minPrice, price);
	}
	return maxProfit;
};
```

### 70. Climbing Stairs

```typescript
const climbStairs = (n: number): number => {
	if (n === 1) return 1;

	const memo: number[] = [n + 1];

	memo[1] = 1;
	memo[2] = 2;

	for (let i = 3; i <= n; i++) {
		memo[i] = memo[i - 1] + memo[i - 2];
	}

	return memo[n];
};
```

## Bit Manipulation

### 268. Missing Number

#### Bit Manipulation Solution

```typescript
const missingNumber = (nums: number[]): number => {
	if (!nums.length) return null;

	let missingNum: number = nums.length;

	for (const num of nums) {
		missingNum ^= num;
	}

	for (let i = 0; i < nums.length; i++) {
		missingNum ^= i;
	}

	return missingNum;
};
```

#### Gauss's Formula

```typescript
const missingNumber = (nums: number[]): number => {
	const expectedSum: number = (nums.length * (nums.length + 1)) / 2;
	const actualSum: number = nums.reduce((result, num) => result + num, 0);
	return expectedSum - actualSum;
};
```

### 136. Single Number

```typescript
const singleNumber = (nums: number[]): number => {
	let singleNumber: number = 0;

	for (const num of nums) {
		singleNumber ^= num;
	}

	return singleNumber;
};
```

## Hash Maps

### 1. Two-Sum

```javascript
const twoSum = (nums, target) => {
	const map = {};

	for (let i = 0; i < nums.length; i++) {
		let thisNum = nums[i];
		map[thisNum] = i;
	}
	for (let i = 0; i < nums.length; i++) {
		let diff = target - nums[i];
		if (map.hasOwnProperty(diff) && map[diff] !== i) {
			return [i, map[diff]];
		}
	}
};
```

## Trees

### 111. Minimum Depth of Binary Tree (BFS)

```javascript
const minDepth = root => {
	if (!root) return 0;
	if (!root.left) return minDepth(root.right) + 1;
	if (!root.right) return minDepth(root.left) + 1;
	return Math.min(minDepth(root.left), minDepth(root.right)) + 1;
};
```

### 104. Maximum Depth of Binary Tree (DFS)

```javascript
const maxDepth = root => {
	const checkDepth = (node, depth) => {
		if (node === null) return depth;
		depth++;
		const leftSide = checkDepth(node.left, depth);
		const rightSide = checkDepth(node.right, depth);
		return Math.max(leftSide, rightSide);
	};
	return checkDepth(root, 0);
};
```

### 700. Search in a Binary Search Tree

```javascript
const searchBST = (root, val) => {
	if (!root) return null;
	if (root.val === val) return root;
	if (root.val > val) return searchBST(root.left, val);
	if (root.val < val) return searchBST(root.right, val);
};
```

### 617. Merge Two Binary Trees

```javascript
const mergeTrees = (t1, t2) => {
	if (!t1 || !t2) return t1 || t2;
	t1.val += t2.val;
	t1.left = mergeTrees(t1.left, t2.left);
	t1.right = mergeTrees(t1.right, t2.right);
	return t1;
};
```

### 938. Range Sum of BST

```javascript
const rangeSumBST = (root, low, high) => {
	if (!root) return 0;
	if (root.val < low) return rangeSumBST(root.right, low, high);
	if (root.val > high) return rangeSumBST(root.left, low, high);
	return root.val + rangeSumBST(root.left, low, high) + rangeSumBST(root.right, low, high);
};
```

## Intervals

### 252. Meeting Rooms

```typescript
const canAttendMeetings = (intervals: number[][]): boolean => {
	const arr = intervals.sort((a, b) => a[0] - b[0]);

	for (let i = 1; i < arr.length; i++) {
		if (arr[i][0] < arr[i - 1][1]) return false;
	}
	return true;
};
```

## Linked Lists

### 21. Merge Two Sorted Lists

```typescript
const mergeTwoLists = (l1: ListNode | null, l2: ListNode | null): ListNode | null => {
	let dummy = new ListNode(NaN);
	let curr = dummy;

	while (l1 && l2) {
		if (l1.val < l2.val) {
			curr.next = l1;
			l1 = l1.next;
		} else {
			curr.next = l2;
			l2 = l2.next;
		}

		curr = curr.next;
	}

	if (l1) {
		curr.next = l1;
	}

	if (l2) {
		curr.next = l2;
	}

	return dummy.next;
};
```

### 328. Odd Even Linked List

```javascript
const oddEvenList = head => {
	if (!head) return null;

	let oddList = new ListNode(-1);
	let evenList = new ListNode(-1);
	let oddStart = oddList;
	let evenStart = evenList;
	let placeValue = 1;
	let current = head;
	while (current) {
		if (placeValue % 2 === 1) {
			oddList.next = current;
			oddList = oddList.next;
		} else {
			evenList.next = current;
			evenList = evenList.next;
		}
		placeValue++;
		current = current.next;
	}

	oddList.next = evenStart.next;
	evenList.next = null;

	return oddStart.next;
};
```

### 19. Remove the nth Node from End of the List

```javascript
const removeNthFromEnd = (head, n) => {
	let fast = head;
	let slow = head;
	while (n > 0) {
		n--;
		fast = fast.next;
	}
	let prev = null;
	while (fast != null) {
		fast = fast.next;
		prev = slow;
		slow = slow.next;
	}
	if (prev == null) {
		return head.next;
	}
	prev.next = slow.next;
	slow.next = null;
	return head;
};
```

### 160. Intersection of Two Linked Lists

```javascript
const getIntersectionNode = (headA, headB) => {
	if (!headA || !headB) return null;
	let pointerA = headA;
	let pointerB = headB;

	while (pointerA && pointerB && pointerA !== pointerB) {
		pointerA = pointerA.next;
		pointerB = pointerB.next;

		if (pointerA === pointerB) return pointerA;
		if (!pointerA) pointerA = headA;
		if (!pointerB) pointerB = headB;
	}
	return pointerA;
};
```

### 142. Linked List Cycle II

```javascript
const detectCycle = head => {
	//hare is the fast pointer and tortoise is the slow pointer
	//Floyd's Algorithm
	let hare = head;
	let tortoise = head;
	while (hare && hare.next) {
		tortoise = tortoise.next;
		hare = hare.next.next;
		if (hare === tortoise) {
			tortoise = head;
			while (tortoise !== hare) {
				tortoise = tortoise.next;
				hare = hare.next;
			}
			return hare;
		}
	}
	return null;
};
```

### 141. Linked List Cycle

```javascript
const hasCycle = head => {
	let slow = head;
	let fast = head;
	while (fast && fast.next) {
		slow = slow.next;
		fast = fast.next.next;
		if (slow === fast) return true;
	}
	return false;
};
```

```typescript
const hasCycle = (head: ListNode | null): boolean => {
	let tortoise: ListNode = head;
	let hare: ListNode = head;

	while (hare && hare.next) {
		hare = hare.next.next;
		tortoise = tortoise.next;
		if (hare === tortoise) return true;
	}

	return false;
};
```

### 21. Merge Two Sorted Lists

```javascript
const mergeTwoLists = (l1, l2) => {
	let dummyhead = new ListNode();
	let curr = dummyhead;

	while (l1 && l2) {
		if (l1.val < l2.val) {
			curr.next = l1;
			l1 = l1.next;
		} else {
			curr.next = l2;
			l2 = l2.next;
		}
		curr = curr.next;
	}
	while (l1) {
		curr.next = l1;
		l1 = l1.next;
		curr = curr.next;
	}
	while (l2) {
		curr.next = l2;
		l2 = l2.next;
		curr = curr.next;
	}
	return dummyhead.next;
};
```

### 234. Palindrome Linked List

```javascript
// Stack Solution

const isPalindrome = head => {
	const stack = [];

	let curr = head;
	while (curr) {
		stack.push(curr.val);
		curr = curr.next;
	}

	while (head) {
		const top = stack.pop();
		if (head.val !== top) return false;

		head = head.next;
	}

	return true;
};

// Reverse Linked List Solution

const isPalindrome = head => {
	if (!head) return true;
	const copyHead = copy(head);
	const reversedHead = reverse(copyHead);
	return isEqual(head, reversedHead);
};

const isEqual = (l1, l2) => {
	while (l1 && l2) {
		if (l1.val !== l2.val) {
			return false;
		}

		l1 = l1.next;
		l2 = l2.next;
	}

	return !l1 && !l2;
};

const reverse = head => {
	let prev = null;
	let next = null;
	while (head) {
		next = head.next;
		head.next = prev;
		prev = head;
		head = next;
	}
	return prev;
};

const copy = head => {
	const copyHead = new ListNode(head.val);
	let copyCurr = copyHead;
	head = head.next;

	while (head) {
		copyCurr.next = new ListNode(head.val);
		copyCurr = copyCurr.next;
		head = head.next;
	}

	return copyHead;
};
```

```typescript
const isPalindrome = (head: ListNode | null): boolean => {
	const copyHead = copyList(head);
	const reverseCopyHead = reverse(copyHead);
	return isEqual(head, reverseCopyHead);
};

const isEqual = (list1: ListNode | null, list2: ListNode | null): boolean => {
	while (list1 && list2) {
		if (list1.val !== list2.val) {
			return false;
		}

		list1 = list1.next;
		list2 = list2.next;
	}

	return !list1 && !list2;
};

const reverse = (node: ListNode | null): ListNode => {
	let curr = node;
	let prev = null;
	let next = null;

	while (curr) {
		next = curr.next;
		curr.next = prev;
		prev = curr;
		curr = next;
	}

	return prev;
};

const copyList = (node: ListNode | null): ListNode => {
	let curr = node;
	let dummy = new ListNode(NaN);
	let prev = dummy;
	while (curr) {
		const copy = new ListNode(curr.val);
		prev.next = copy;
		prev = prev.next;
		curr = curr.next;
	}
	return dummy.next;
};
```

### 83. Remove Duplicates from Sorted List

```javascript
const deleteDuplicates = head => {
	if (!head) return null;
	let current = head;
	while (current && current.next) {
		if (current.val === current.next.val) {
			current.next = current.next.next;
		} else {
			current = current.next;
		}
	}
	return head;
};
```

```typescript
const deleteDuplicates = (head: ListNode | null): ListNode | null => {
	if (!head || !head.next) return head;
	let prev = head;
	let forward = head.next;
	while (forward) {
		if (forward.val === prev.val) {
			prev.next = forward.next;
			forward = forward.next;
		} else {
			prev = forward;
			forward = forward.next;
		}
	}

	return head;
};
```

### 203. Remove Linked List Elements

```javascript
const removeElements = (head, val) => {
	const dummy = new ListNode(NaN);
	dummy.next = head;

	let current = dummy;
	while (current && current.next) {
		const next = current.next;
		if (next.val === val) {
			current.next = current.next.next;
		} else {
			current = current.next;
		}
	}

	return dummy.next;
};
```

```typescript
const removeElements = (head: ListNode | null, val: number): ListNode | null => {
	const dummy = new ListNode(NaN);
	dummy.next = head;

	let current = dummy;
	while (current && current.next) {
		const next = current.next;
		if (next.val === val) {
			current.next = current.next.next;
		} else {
			current = current.next;
		}
	}

	return dummy.next;
};
```

### 206. Reverse a Linked List

```javascript
const reverseList = head => {
	let curr = head;
	let prev = null;
	let nextTemp = null;

	while (curr) {
		nextTemp = curr.next;
		curr.next = prev;
		prev = curr;
		curr = nextTemp;
	}
	return prev;
};
```

### 237. Delete Node in a Linked List

```javascript
const deleteNode = node => {
	node.val = node.next.val;
	node.next = node.next.next;
};
```

### 876. Middle of the Linked List

```javascript
const middleNode = head => {
	let fast = head;
	let slow = head;

	while (fast && fast.next) {
		fast = fast.next.next;
		slow = slow.next;
	}
	return slow;
};
```

```typescript
const middleNode = (head: ListNode | null): ListNode | null => {
	let hare: ListNode = head;
	let tortoise: ListNode = head;

	while (hare && hare.next) {
		hare = hare.next.next;
		tortoise = tortoise.next;
	}

	return tortoise;
};
```

### Convert Binary Number in a Linked List to Integer

```javascript
const getDecimalValue = head => {
	const result = [];
	while (head) {
		result.push(String(head.val));
		head = head.next;
	}
	return parseInt(result.join(""), 2);
};
```

## Binary Search

### 744. Find Smallest Letter Greater Than Target

```typescript
const nextGreatestLetter = (letters: string[], target: string): string => {
	let left: number = 0;
	let right: number = letters.length - 1;

	while (left < right) {
		let mid: number = Math.floor((left + right) / 2);
		if (letters[mid] <= target) {
			left = mid + 1;
		} else {
			right = mid;
		}
	}

	return letters[left] <= target ? letters[0] : letters[left];
};
```

### 704. Binary Search

```typescript
const search = (nums: number[], target: number): number => {
	let left: number = 0;
	let right: number = nums.length;

	while (left < right) {
		let mid: number = Math.floor((left + right) / 2);
		if (nums[mid] < target) {
			left = mid + 1;
		} else {
			right = mid;
		}
	}

	return nums[left] === target ? left : -1;
};
```

### 1351. Count Negative Numbers in a Sorted Matrix

```javascript
const countNegatives = grid => {
	let count = 0;
	for (let i = 0; i < grid.length; i++) {
		for (let j = 0; j < grid[i].length; j++) {
			if (Math.sign(grid[i][j]) === -1) count++;
		}
	}
	return count;
};
```

## Arrays

### 448. Find All Numbers Disappeared in an Array

```typescript
const findDisappearedNumbers = (nums: number[]): number[] => {
	const result: number[] = [];
	const numberSet = new Set(nums);

	for (let i = 1; i <= nums.length; i++) {
		if (!numberSet.has(i)) result.push(i);
	}

	return result;
};
```

### 217. Contains Duplicate

```javascript
const containsDuplicate = nums => {
	const numSet = new Set(nums);
	return numSet.size !== nums.length;
};
```

### Remove Element

```javascript
// Pointer Solution
const removeElement = (nums, val) => {
	let pointer = 0;
	for (let i = 0; i < nums.length; i++) {
		if (nums[i] !== val) {
			nums[pointer] = nums[i];
			pointer++;
		}
	}
	return pointer;
};

// Splice Solution
const removeElement = (nums, val) => {
	for (let i = nums.length - 1; i >= 0; i--) {
		if (nums[i] === val) nums.splice(i, 1);
	}
	return nums.length;
};
```

### Merge Sorted Array

```javascript
const merge = (nums1, m, nums2, n) => {
	let first = m - 1;
	let second = n - 1;

	for (let i = m + n - 1; i >= 0; i--) {
		if (second < 0) break;
		if (nums1[first] > nums2[second]) {
			nums1[i] = nums1[first];
			first--;
		} else {
			nums1[i] = nums2[second];
			second--;
		}
	}
};
```

### Duplicate Zeros

```javascript
const duplicateZeros = arr => {
	for (let i = 0; i < arr.length; i++) {
		if (!arr[i]) {
			arr.splice(i, 0, 0);
			i++;
			arr.pop();
		}
	}
};
```

## SQL

### 613. Shortest Distance in a Line

```sql
SELECT MIN(ABS(P2.x - P1.x)) AS shortest
FROM point AS P1, point AS P2
WHERE P1.x <> P2.x;
```

### 1571. Warehouse Manager

```sql
SELECT W.name AS warehouse_name, SUM(units * volume) AS volume
FROM Warehouse AS W
JOIN (SELECT product_id, Width * Length * Height AS volume
     FROM Products) AS P
USING (product_id)
GROUP BY W.name;
```

### 596. Classes More Than 5 Students

```sql
SELECT class
FROM courses
GROUP BY class
HAVING COUNT(DISTINCT student) >= 5
```

### 176. Second Highest Salary

```sql
SELECT MAX(Salary) AS SecondHighestSalary
FROM Employee
WHERE Salary < (
    SELECT MAX(Salary)
    FROM Employee
)
```

### 1729. Find Followers Count

```sql
SELECT F.user_id, COUNT(F.follower_id) AS followers_count
FROM Followers AS F
GROUP BY F.user_id
ORDER BY F.user_id;
```

### 1173. Immediate Food Delivery I

```sql
SELECT ROUND(SUM(D.order_date = D.customer_pref_delivery_date) * 100 / COUNT(D.delivery_id), 2) AS immediate_percentage
FROM Delivery AS D;
```

### 181. Employees Earning More Than Their Managers

```sql
SELECT E.name AS Employee
FROM Employee AS E
JOIN Employee AS E2
ON E.ManagerID = E2.Id
WHERE E.Salary > E2.Salary
```

### 610. Triangle Judgement

```sql
SELECT T.x, T.y, T.z,
IF(T.x + T.y > T.z AND T.y + T.z > T.x AND T.z + T.x > T.y, 'Yes', 'No') AS triangle
FROM triangle AS T
```

### 182. Duplicate Emails

```sql
SELECT P.Email
FROM Person AS P
GROUP BY P.Email
HAVING COUNT(P.Email) > 1
```

### 1303. Find the Team Size

```sql
SELECT E1.employee_id, E2.team_size
FROM Employee AS E1
JOIN (
    SELECT team_id, COUNT(1) AS team_size
    FROM Employee
    GROUP BY team_id
    ) AS E2
ON E1.team_id = E2.team_id;
```

### 1350. Students With Invalid Departments

```sql
SELECT S.id, S.name
FROM Students AS S
LEFT JOIN Departments AS D
ON D.id = S.department_id
WHERE D.name IS Null AND D.id IS NULL;
```

### 603. Consecutive Available Seats

```sql
SELECT DISTINCT C1.seat_id
FROM cinema AS C1, cinema AS C2
WHERE C1.free = 1
AND C2.free = 1
AND (C2.seat_id = C1.seat_id + 1 OR C2.seat_id = C1.seat_id -1);
```

### 1082. Sales Analysis I

```sql
SELECT S.seller_id
FROM Sales AS S
GROUP BY S.seller_id
HAVING SUM(S.price) = (
    SELECT SUM(S.price)
    FROM Sales AS S
    GROUP BY S.seller_id
    ORDER BY SUM(S.price) desc
    LIMIT 1
);
```

### 1495. Friendly Movies Streamed Last Month

```sql
SELECT DISTINCT C.title
FROM Content AS C
JOIN TVProgram AS TVP
ON TVP.content_id = C.content_id
WHERE C.content_type = 'Movies'
AND TVP.program_date BETWEEN '2020-06-01' AND '2020-06-30'
AND C.Kids_content = 'Y';
```

### 1148. Article Views I

```sql
SELECT author_id AS id
FROM Views
WHERE author_id = viewer_id
GROUP BY author_id
ORDER BY author_id;
```

### 1565. Unique Orders and Customers Per Month

```sql
SELECT LEFT(order_date, 7) AS month,
COUNT(order_id) AS order_count,
COUNT(DISTINCT customer_id) AS customer_count
FROM Orders
WHERE invoice > 20
GROUP BY LEFT(order_date, 7)
ORDER BY month;
```

### 175. Combine Two Tables

```sql
SELECT P.FirstName, P.LastName, A.City, A.State
FROM Person AS P
LEFT JOIN Address AS A
ON P.PersonId = A.PersonId
```

### 1280. Students and Examinations

```sql
SELECT stu.student_id, stu.student_name, sub.subject_name, SUM(e.subject_name IS NOT NULL) AS attended_exams
FROM Students AS stu
JOIN Subjects AS sub
LEFT JOIN Examinations AS e
ON stu.student_id = e.student_id AND sub.subject_name = e.subject_name
GROUP BY stu.student_name, sub.subject_name
ORDER BY stu.student_id, sub.subject_name
```

### 511. Game Play Analysis I

```sql
SELECT A.player_id, MIN(A.event_date) AS first_login
FROM Activity AS A
GROUP BY A.player_id;
```

### 512. Game Play Analysis II

```sql
SELECT A.player_id, A.device_id
FROM Activity AS A, (
    SELECT A2.player_id, MIN(A2.event_date) AS Min_Date
    FROM Activity AS A2
    GROUP BY A2.player_id
) AS Derived_Table
WHERE A.player_id=Derived_Table.player_id and A.event_date=Derived_Table.Min_Date
```

### 1623. All Valid Triplets That Can Represent a Country

```sql
SELECT A.student_name AS member_A, B.student_name AS member_B, C.student_name AS member_C
FROM SchoolA AS A
JOIN SchoolB AS B
ON A.student_id <> B.student_id AND A.student_name <> B.student_name
JOIN SchoolC AS C
ON A.student_id <> C.student_id AND B.student_id <> C.student_id
AND A.student_name <> C.student_name
AND B.student_name <> C.student_name;
```

### 1407. Top Travellers

```sql
SELECT name, IFNULL(SUM(distance), 0) AS travelled_distance
FROM Users as U
LEFT JOIN Rides as R
ON R.user_id = U.id
GROUP BY U.id
ORDER BY travelled_distance desc, name asc
```

### 1050. Actors and Directors Who Cooperated At Least Three Times

```sql
SELECT actor_id, director_id
FROM ActorDirector
GROUP BY actor_id, director_id
HAVING COUNT(actor_id) >= 3
```

### 197. Rising Temperature

```sql
SELECT W.id
FROM Weather as W
JOIN Weather as W2
ON DATEDIFF(W.recordDate, W2.recordDate) = 1
AND W.temperature > W2.temperature;
```

### 620. Not Boring Movies

```sql
SELECT *
FROM cinema
WHERE id % 2 != 0 and description <> 'boring'
order by rating desc;
```

### 595. Big Countries

```sql
SELECT name, population, area
FROM World
WHERE area > 3000000 or population > 25000000
```

### 1683. Invalid Tweets

```sql
SELECT T.tweet_id
FROM Tweets AS T
WHERE LENGTH(T.content) > 15;
```

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

# InterviewBit

## SQL

### Actors and Their Movies

```sql
SELECT M.movie_title
FROM movies AS M
RIGHT JOIN movies_cast AS MC
USING (movie_id)
WHERE MC.actor_id = (
    SELECT MC.actor_id
    FROM movies_cast AS MC
    GROUP BY MC.actor_id
    HAVING COUNT(MC.actor_id) > 1
)
```

### Short Films

```sql
SELECT m.movie_title,
    m.movie_year,
    CONCAT(director_first_name, director_last_name) AS "director_name",
    CONCAT(actor_first_name, actor_last_name) AS "actor_name",
    mc.role
FROM movies AS m
JOIN movies_cast as mc
ON mc.movie_id = m.movie_id
JOIN actors AS a
ON a.actor_id = mc.actor_id
JOIN movies_directors AS md
ON md.movie_id = m.movie_id
JOIN directors AS d
ON d.director_id = md.director_id
ORDER BY m.movie_time ASC
LIMIT 1

--I put in ASC just to remind myself of what is going on
```

### Neutral Reviewers

```sql
SELECT r.reviewer_name
FROM reviewers as r
JOIN ratings as ra
ON r.reviewer_id = ra.reviewer_id
WHERE ra.reviewer_stars IS NULL;
```

### Movie Character

```sql
SELECT CONCAT(d.director_first_name, d.director_last_name) AS director_name, m.movie_title
FROM movies AS m
JOIN movies_directors AS md
ON md.movie_id = m.movie_id
JOIN directors AS d
ON d.director_id = md.director_id
JOIN movies_cast AS mc
ON m.movie_id = mc.movie_id
WHERE mc.role = 'SeanMaguire'
```

# Code Katas

## Unique In Order

```javascript
var uniqueInOrder = function (iterable) {
	const result = [];
	let prevChar = "";

	for (const char of iterable) {
		if (prevChar !== char) {
			prevChar = char;
			result.push(char);
		}
	}

	return result;
};
```

## A Square of Squares

```javascript
const isSquare = num => {
	const rootNum = Math.sqrt(num);
	if (rootNum % 2 === 0 || (rootNum % 2 === 1 && num >= 0)) {
		return true;
	} else {
		return false;
	}
};
```

## Training on Dubstep

```javascript
const songDecoder = dubStepSong => {
	const splitArray = dubStepSong.split("WUB");
	const filteredArray = splitArray.filter(character => {
		if (character !== "") {
			return true;
		} else {
			return false;
		}
	});
	return filteredArray.join(" ");
};

console.log(songDecoder("WUBWEWUBAREWUBWUBTHEWUBCHAMPIONSWUBMYWUBFRIENDWUB"));
```

## Create Phone Number

```javascript
const createPhoneNumber = nums => {
	const phoneNumber = [];
	const sectionOne = ["(", nums[0], nums[1], nums[2], ")"];
	const sectionTwo = [" ", nums[3], nums[4], nums[5], "-"];
	const sectionThree = [nums[6], nums[7], nums[8], nums[9]];
	return [...sectionOne, ...sectionTwo, ...sectionThree].join("");
};

console.log(createPhoneNumber([6, 6, 0, 8, 6, 4, 4, 6, 7, 8]));
```

## Training on Roman Numerals

```javascript
const solution = romanNum => {
	const numerals = {
		M: 1000,
		D: 500,
		C: 100,
		L: 50,
		X: 10,
		V: 5,
		I: 1,
	};
	const numbers = romanNum.split("");
	let solution = 0;
	let precedingNumeral;
	for (const ele of numbers) {
		if (precedingNumeral < numerals[ele]) {
			solution += numerals[ele] - 2;
		} else {
			solution += numerals[ele];
		}
		precedingNumeral = numerals[ele];
	}
	return solution;
};

solution("IX");
```

## Convert String to Camel Case

```javascript
const toCamelCase = str => {
	const splitStr = str.split("");
	const result = [];
	let underscorePresent = false;
	for (const ele of splitStr) {
		if (ele === "_" || ele === "-") {
			result.unshift();
			underscorePresent = true;
		} else {
			if (underscorePresent) {
				result.push(ele.toUpperCase());
				underscorePresent = false;
			} else {
				result.push(ele);
			}
		}
	}
	return result.join("");
};

console.log(toCamelCase("the_camel_and_the_snake"));
```

### Convert Camel Case to Snake Case

-   This is my own original challenge

```javascript
const toSnakeCase = str => {
	const splitStr = str.split("");
	const result = [];
	for (const ele of splitStr) {
		if (ele === ele.toUpperCase()) {
			result.push("_", ele.toLowerCase());
		} else {
			result.push(ele);
		}
	}
	return result.join("");
};

console.log(toSnakeCase("theCamelAndTheSnake"));
```
