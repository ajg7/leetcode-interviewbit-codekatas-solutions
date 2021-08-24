## Linked Lists

### 21. Merge Two Sorted Lists

```javascript
const mergeTwoLists = (l1, l2) => {
    const dummy = new ListNode(NaN);
    let curr = dummy;
    
    while (l1 && l2) {
        if (l1.val > l2.val) {
            curr.next = l2;
            l2 = l2.next;
        } else {
            curr.next = l1;
            l1 = l1.next;
        }
        
        curr = curr.next;
    }
    
    if (l1) {
        curr.next = l1;
    } else {
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

### 206. Reverse Linked List

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
