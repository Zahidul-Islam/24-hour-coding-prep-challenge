# Linked Lists

## Linked List `node`
```javascript
class Node {
  constructor(value, next = null) {
    this.value = value;
    this.next = next;
  }
}
```

## Print a `linked list`
```javascript
function print(node) {
  while(node !== null) {
      console.log('->' + node.value);
      node = node.next;
  }
}
```

### 1. Remove Dups: Write code to remove duplicates from an unsorted linked list. 

```javascript
function removeDups(node) {
  if(node === null) return null;
  
  let nodes = new Map();
  let current = node.next;
  let prev = node;
  nodes.set(node.value, 1);
  
  while(current !== null) {
    if(nodes.get(current.value) === 1) {
      prev.next = current.next;
    } else {
      nodes.set(current.value, 1);
      prev = current;
    }
    current = current.next;
  }
  return node;
}

let node1 = new Node(1);
let node2 = new Node(2);
let node3 = new Node(3);
let node4 = new Node(2);
let node5 = new Node(1);

node1.next = node2;
node2.next = node3;
node3.next = node4;
node4.next = node5;
node5.next = null;

print(removeDups(node1));

/* 
"->1"
"->2"
"->3"
*/
```

### 2. Return Kth to Last: Implement an algorithm to find the kth to last element of a singly linked list. 

```javascript
function KthToLast(root, n) {
  if(!root) return null;
  let current = root;
  let follower = root;
  
  for(let i = 0; i < n; i++) {
    current = current.next;
  }
  
  while(current.next !== null) {
    current = current.next;
    follower = follower.next;
  }
  
  return follower;
}


let node1 = new Node(1);
let node2 = new Node(2);
let node3 = new Node(3);
let node4 = new Node(4);
let node5 = new Node(5);

node1.next = node2;
node2.next = node3;
node3.next = node4;
node4.next = node5;
node5.next = null;

console.log(KthToLast(node1, 2).value);  // 3
```

### 3. Delete middle of linked list 

```javascript
function removeDups(head) {
  if(head === null) return null;
  
  let fast = head;
  let slow = head;
  let prev = null;
  
  while(fast !== null && fast.next !== null) {
    fast = fast.next.next;
    prev = slow;
    slow = slow.next;
  }
  
  prev.next = slow.next;
  
  return head;
}

let nodeA = new Node('a');
let nodeB = new Node('b');
let nodeC = new Node('c');
let nodeD = new Node('d');
let nodeE = new Node('e');
let nodeF = new Node('f');

nodeA.next = nodeB;
nodeB.next = nodeC;
nodeC.next = nodeD;
nodeD.next = nodeE;
nodeE.next = nodeF;
nodeF.next = null;

print(removeDups(nodeA)); 
/*
"->a"
"->b"
"->c"
"->e"
"->f"
*/
```
### 4. Partitioning a linked list around a given value and If we don’t care about making the elements of the list `stable`

```javascript
function partition(head, x) {
  let tail = head;
  let current = head;
  
  while(current !== null) {
    let next = current.next;
    if(current.value < x) {
      current.next = head;
      head = current;
    } else {
      tail.next = current;
      tail = current;
    }
    current = next;
  }
  tail.next = null;
  
  return head;
}

let nodeA = new Node(3);
let nodeB = new Node(5);
let nodeC = new Node(8);
let nodeD = new Node(2);
let nodeE = new Node(10);
let nodeF = new Node(2);
let nodeH = new Node(1);

nodeA.next = nodeB;
nodeB.next = nodeC;
nodeC.next = nodeD;
nodeD.next = nodeE;
nodeE.next = nodeF;
nodeF.next = nodeH;
nodeH.next = null;

print(partition(nodeA, 5));
/*
"->1"
"->2"
"->2"
"->3"
"->5"
"->8"
"->10"
*/

```

### 5. Given a linked list where each node has two pointers, one to the next node and one to a random node in the list, clone the linked list.

```javascript
function clone(node) {
  if(node === null) return node;
  let current = node;
  
  //copy every node and insert to list
  while(current !== null) {
    let copy = new Node(current.value);
    copy.next = current.next;
    current.next = copy;
    current = copy.next;
  }
  
  //copy random pointer for each new node
  current = node;
  while(current !== null) {
    if(current.random !== null) {
      current.next.random = current.random.next;
    }
    current = current.next.next;
  }
  
  //break list into two
  current = node;
  let newHead = node.next;
  while(current !== null) {
    let temp = current.next;
    current.next = temp.next;
    if(temp.next !== null) {
      temp.next = temp.next.next;
    }
    current = current.next;
  }
  
  return newHead;
}

//Using Map
function clone(node) {
  if(node === null) return node;
 
  let map = new Map();
  let copy = new Node(node.value);
  let current = node;
  let newHead = copy;
  
  map.set(current, copy);
  
  current = current.next;
  while(current !== null) {
    let temp = new Node(current.value);
    map.set(current, temp);
    copy.next = temp;
    copy = temp;
    current = current.next;
  }
  
  current = node;
  copy = newHead;
  
  while(current !== null) {
    if(current.randome !== null) {
      copy.random = map.get(current.random);
    } else {
      copy.random = null;
    }
    
    current = current.next;
    copy = copy.next;
  }
  
  return newHead;
}
```

### 6. Given a linked list, determine whether it contains a cycle.

```javascript
function hasCycle(node) {
  if(node === null) return false;
  let slow = node;
  let fast = node.next;
  
  while(fast !== null && fast.next !== null) {
    if(fast === slow) return true;
    slow = slow.next;
    fast = fast.next.next;
  }
  
  return false;
}

let node1 = new Node(1);
let node2 = new Node(2);
let node3 = new Node(3);
let node4 = new Node(4);
let node5 = new Node(5);

node1.next = node2;
node2.next = node3;
node3.next = node4;
node4.next = node5;
node5.next = node3;

console.log(hasCycle(node1));
```

### 7. How to find middle element of linked list in one pass?

```javascript
function findMiddle(node) {
    if(node === null) return null;
    let fast = node.next;
    let slow = node;
    
    while(fast !== null && fast.next !== null) {
        fast = fast.next.next;
        slow = slow.next;
    }
    console.log(slow.value);
}

let node1 = new Node(5);
let node2 = new Node(6);
let node3 = new Node(7);
let node4 = new Node(1);
let node5 = new Node(2);

node1.next = node2;
node2.next = node3;
node3.next = node4;
node4.next = node5;
node5.next = null;

findMiddle(node1); //> 7
```

#### 8. Add Two Numbers

```javascript
// Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
// Output: 7 -> 0 -> 8
// Explanation: 342 + 465 = 807.

const addTwoNumbers = function(l1, l2) {
  let head = new Node(0);
  let carry = 0;
  let current = head;
  
  while(l1 !== null || l2 !== null ) {
    const x = l1 !== null ? l1.value : 0;
    const y = l2 !== null ? l2.value : 0;
        
    const sum = carry + x + y;
    carry = Math.floor(sum / 10);
        
    current.next = new Node(sum % 10);
    current = current.next;
        
    if(l1 != null) l1 = l1.next;
    if(l2 != null) l2 = l2.next;
  }
    
  if (carry > 0) {
    current.next = new ListNode(carry);
  }
  return head.next;
};

const node13 = new Node(3);
const node12 = new Node(4);
const node11 = new Node(2);
node11.next = node12;
node12.next = node13;
const l1 = node11; 

const node23 = new Node(4);
const node22 = new Node(6);
const node21 = new Node(5);
node22.next = node23;
node21.next = node22;
const l2 = node21;

print(addTwoNumbers(l1, l2));
/*
"->7"
"->0"
"->8"
*/
```