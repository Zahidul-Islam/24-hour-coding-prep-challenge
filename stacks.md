# Stacks

#### 1. Given a stack sort the elements in the stack using no more than ane additional stack

```javascript
Array.prototype.peek = function() {
  return this[this.length -1];
}

Array.prototype.isEmpty = function() {
  return this.length <= 0;
}

function sortStack(stack) {
  if(!stack || stack.length ===0) return stack;
  
  let newStack = [];
  newStack.push(stack.pop());
  
  while(!stack.isEmpty()) {
    const temp = stack.pop();
    while(!newStack.isEmpty() && temp > newStack.peek()) {
      stack.push(newStack.pop());
    }
    newStack.push(temp);
  }
  return newStack;
}

console.log(sortStack([5, 1, 3, 2, 4])); // [5, 4, 3, 2, 1]
```

#### 2. Evaluate Reverse Polish Notation in Javascript

```javascript
function reversePolishNotation(seq) {
  if(seq.length <= 2) {
    return;
  }
  
  const operands = ['+', '-', '*', '/'];
  const stack = [];
  let i = 0;
  
  stack.push(seq[i]);
  i++;
  
  while(i <= seq.length) {
    let item = seq[i];
    let index = operands.indexOf(item);
    
    if(index < 0) {
      stack.push(item);
    } else {
      const a = parseInt(stack.pop(), 10);
      const b = parseInt(stack.pop(), 10);
        
      if(index === 0) {
        stack.push(a + b);
      } 
      if(index === 1) {
        stack.push(a - b);
      }
      if(index === 2) {
        stack.push(a * b);
      }
      if(index === 3) {
        stack.push(b/a);
      }
    }
    i++;
  }
  
  return parseInt(stack[0], 0);
}

console.log(reversePolishNotation(["2", "1", "+", "3", "*"])) // 9
console.log(reversePolishNotation(["4", "13", "5", "/", "+"])) // 6
console.log(reversePolishNotation(["10", "6", "9", "3", "+", "-11", "*", "/", "*", "17", "+", "5", "+"])) // 22
console.log(reversePolishNotation(["2", "1"])) // undefined
```

#### 3. Implement a stack using javascript

```javascript
function Stack() {
  this.top = null;
}

Stack.prototype.push = function (val) {
  let node = {
    data : val,
    next : null
  };
  
  node.next = this.top;
  this.top = node;
};

Stack.prototype.pop = function () {
  if(this.top === null) {
    return null;
  } else {
    const top = this.top;
    this.top = this.top.next;
    return top.data;
  }
};

Stack.prototype.peek = function() {
  if(this.top === null) {
    return null;
  } else {
    return this.top.data;
  }
}

var S1 = new Stack();
S1.push(5);
S1.push(6);
S1.push(7);
S1.push(8);

console.log(S1.pop()); // 8
console.log(S1.pop()); // 7
```

#### 4. Queue using two stacks javascript

```javascript
function Queue() {
  this.pushStack = new Stack();
  this.popStack = new Stack();
}

Queue.prototype.enqueue = function(value) {
  this.pushStack.push(value);
}

Queue.prototype.dequeue = function() {
  let popStack = this.popStack;
  let pushStack = this.pushStack;
  
  if(popStack.peek()) {
    const deq = popStack.pop();
    return deq;
  }
  
  while(pushStack.peek()) {
    popStack.push(pushStack.pop());
  }
}

const q1 = new Queue();
q1.enqueue(3);
q1.enqueue(4);
q1.enqueue(5);
q1.enqueue(6);
q1.enqueue(7);
q1.dequeue();
q1.dequeue();
q1.dequeue();

console.log(q1);
```

#### 5.

```javascript
function stepsToSolveTowerOfHanoi(height, from, to, via) {
  if (height >= 1) {
    // Move a tower of height - 1 to buffer peg using destination peg
    stepsToSolveTowerOfHanoi(height - 1, from, via, to);
    // Move the remaining disk to the destination peg.
    console.log(`Move disk ${height} from Tower ${from} to Tower ${to}`);
    // Move the tower of `height-1` from the `buffer peg` to the `destination peg` using the `source peg`.        
    stepsToSolveTowerOfHanoi(height - 1, via, to, from);
  }
  
  return;
}

stepsToSolveTowerOfHanoi(3, "A", "C", "B");
/*
"Move disk 1 from Tower A to Tower C"
"Move disk 2 from Tower A to Tower B"
"Move disk 1 from Tower C to Tower B"
"Move disk 3 from Tower A to Tower C"
"Move disk 1 from Tower B to Tower A"
"Move disk 2 from Tower B to Tower C"
"Move disk 1 from Tower A to Tower C"
*/
```

#### 6. Justify if a string consists of valid parentheses

```javascript
function isMatchingBrackets(str) {
  if(str.length <= 1) {
    return false;
  }
  
  let stack = [];
  const map = {
    '{': '}',
    '[': ']',
    '(': ')'
  };
  
  for(let char of str) {
    if(char === '(' || char === '[' || char === '{') {
      stack.push(char);
    } else {
      const last = stack.pop();
      if (char !== map[last]) {
        return false;
      }
    }
  }
  return stack.length === 0;
}

console.log(isMatchingBrackets("(){}")); // true
console.log(isMatchingBrackets("[{()()}({[]})]({}[({})])((((((()[])){}))[]{{{({({({{{{{{}}}}}})})})}}}))[][][]")); // true
console.log(isMatchingBrackets("({(()))}}"));  // false
```