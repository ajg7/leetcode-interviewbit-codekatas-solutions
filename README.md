My solutions for leetcode, interviewbit & codekatas

# Leetcode

## SQL

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

## Graphs

### 997. Find the Town Judge
```javascript
const findJudge = (N, trust) => {
    const map = {};
    
    for(const [person1, person2] of trust) {
        if (!map[person1]) map[person1] = { "in": 0, "out": 0 };
        if (!map[person2]) map[person2] = { "in": 0, "out": 0 };
        
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
    }
    return checkDepth(root, 0)
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
    if (root.val < low)  return rangeSumBST(root.right, low, high);
    if (root.val > high) return rangeSumBST(root.left, low, high);
    return root.val + rangeSumBST(root.left, low, high) + rangeSumBST(root.right, low, high);
};
```

## Linked Lists

### 328. Odd Even Linked List
```javascript
const oddEvenList = head => {
    if (!head) return null
    
    let oddList = new ListNode(-1);
    let evenList = new ListNode(-1);
    let oddStart = oddList;
    let evenStart = evenList;
    let placeValue = 1;
    let current = head;
    while (current) {
        if (placeValue % 2 === 1) {
            oddList.next = current;
            oddList = oddList.next
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
    while (n > 0){
        n--;
        fast = fast.next;
    }
    let prev = null;
    while (fast != null){
        fast = fast.next;
        prev = slow;
        slow = slow.next;
    }
    if (prev == null){
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
    return null
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

### 21. Merge Two Sorted Lists
```javascript
const mergeTwoLists = (l1, l2) => {
    let dummyhead = new ListNode();
    let curr = dummyhead;
    
    while (l1 && l2) {
        if (l1.val < l2.val) {
            curr.next = l1;
            l1 = l1.next
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
        curr = curr.next
    }
    return dummyhead.next;
};
```

### 234. Palindrome Linked List
```javascript
// Stack Solution

const isPalindrome = head => {
    const stack = []
    
    let curr = head
    while (curr) {
        stack.push(curr.val)
        curr = curr.next
    }
    
    while (head) {
        const top = stack.pop()
        if (head.val !== top) 
            return false
        
        head = head.next
    }
    
    return true
};

// Reverse Linked List Solution

const isPalindrome = head => {
    if (!head) return true
    const copyHead = copy(head)
    const reversedHead = reverse(copyHead)
    return isEqual(head, reversedHead)
};

const isEqual = (l1, l2) => {
    while (l1 && l2) {
        if (l1.val !== l2.val) {
            return false
        }
        
        l1 = l1.next
        l2 = l2.next
    }
    
    return !l1 && !l2
}

const reverse = head => {
    let prev = null
    let next = null
    while (head) {
        next = head.next
        head.next = prev
        prev = head
        head = next
    }
    return prev
}

const copy = head => {
    const copyHead = new ListNode(head.val)
    let copyCurr = copyHead
    head = head.next
    
    while (head) {
        copyCurr.next = new ListNode(head.val)
        copyCurr = copyCurr.next
        head = head.next
    }
    
    return copyHead
}
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
            current = current.next
        }
    }
    return head
};
```

### 203. Remove Linked List Elements
```javascript
 const removeElements = (head, val) => {
    const dummy = new ListNode(NaN)
    dummy.next = head
    
    let current = dummy
    while (current && current.next) {
        const next = current.next
        if (next.val === val) {
            current.next = current.next.next
        } else {
            current = current.next
        }
    }
    
    return dummy.next
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
    return prev
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
    return slow
};
```

### Convert Binary Number in a Linked List to Integer
```javascript
const getDecimalValue = head => {
    const result = [];
    while (head) {
        result.push(String(head.val));
        head = head.next
    }
    return parseInt(result.join(""), 2)
};
```

## Binary Search

### 1351. Count Negative Numbers in a Sorted Matrix
```javascript
const countNegatives = grid => {
    let count = 0;
    for (let i = 0; i < grid.length; i++) {
        for (let j = 0; j < grid[i].length; j++) {
            if (Math.sign(grid[i][j]) === -1) count++;
        }
    } 
    return count
};
```

## Arrays

### Remove Element
```javascript
// Pointer Solution
const removeElement = (nums, val) => {
    let pointer = 0;
    for (let i = 0; i < nums.length; i++) {
        if (nums[i] !== val) {
            nums[pointer] = nums[i]
            pointer++
        }
    }
    return pointer
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
    let second = n  -1;
    
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
            i++
            arr.pop();
        }  
    }
};
```
# InterviewBit

## 


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
var uniqueInOrder=function(iterable){
  const result = []
  let prevChar = ''
  
  for (const char of iterable) {
    if (prevChar !== char) {
      prevChar = char
      result.push(char)
    }
  }
  
  return result
}
```

## A Square of Squares
```javascript
const isSquare = num => {
  const rootNum = Math.sqrt(num)
  if(rootNum % 2 === 0 || rootNum % 2 === 1 && num >= 0) {
    return true
  } else {
    return false
  }
}
```

## Training on Dubstep
```javascript
const songDecoder = dubStepSong => {
    const splitArray = dubStepSong.split("WUB");
    const filteredArray = splitArray.filter(character => {
      if(character !== "") {
        return true;
      } else {
        return false;
      }
    })
    return filteredArray.join(" ")
}

console.log(songDecoder("WUBWEWUBAREWUBWUBTHEWUBCHAMPIONSWUBMYWUBFRIENDWUB"));
```

## Create Phone Number
```javascript
const createPhoneNumber = nums => {
  const phoneNumber = []
  const sectionOne = ["(", nums[0], nums[1], nums[2], ")"]
  const sectionTwo = [" ", nums[3], nums[4], nums[5], "-"]
  const sectionThree = [nums[6], nums[7], nums[8], nums[9]]
  return [...sectionOne, ...sectionTwo, ...sectionThree].join("")
}



console.log(createPhoneNumber([6,6,0,8,6,4,4,6,7,8]))
```
## Training on Roman Numerals
```javascript
const solution = (romanNum) => {
  const numerals = {
      M: 1000,
      D: 500,
      C: 100,
      L: 50,
      X: 10,
      V: 5,
      I: 1
    };
  const numbers = romanNum.split("");
  let solution = 0;
  let precedingNumeral;
  for (const ele of numbers) {
    if(precedingNumeral < numerals[ele]) {
        solution += numerals[ele] - 2
    } else {
      solution += numerals[ele]
    }
    precedingNumeral = numerals[ele]
  }
  return solution
}

solution("IX")
```

## Convert String to Camel Case
```javascript
const toCamelCase = str => {
  const splitStr = str.split("");
  const result = [];
  let underscorePresent = false;
  	for(const ele of splitStr) {
	    if(ele === "_" || ele === "-") {
		result.unshift()
		underscorePresent = true;
	    } else {
		if(underscorePresent) {
		    result.push(ele.toUpperCase())
		    underscorePresent = false;
		} else {
		    result.push(ele)
		  }
	      }
	    }
   return result.join("")
}

console.log(toCamelCase("the_camel_and_the_snake"))
```
### Convert Camel Case to Snake Case
- This is my own original challenge
```javascript
const toSnakeCase = str => {
  const splitStr = str.split("");
  const result = [];
  for(const ele of splitStr) {
      if(ele === ele.toUpperCase()) {
         result.push("_", ele.toLowerCase())
      } else {
	result.push(ele)
        }
      }
   return result.join("")
}

console.log(toSnakeCase("theCamelAndTheSnake"))
```

