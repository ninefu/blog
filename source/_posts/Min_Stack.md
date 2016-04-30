title: Min Stack
date: 2016-02-01 18:39:22
categories:
- Leetcode
tags:
- Leetcode
- Design
comments: true
---
### Solutions with two stacks

```java
class MinStack {
    Stack<Integer> nums = new Stack<Integer>();
    Stack<Integer> min = new Stack<Integer>();
    
    public void push(int x) {
        nums.push(x);
        if (!min.empty() && min.peek() < x){
            min.push(min.peek());
        }else{
            min.push(x);
        }
    }

    public void pop() {
        if (!nums.empty() && !min.empty()){
            nums.pop();
            min.pop();
        }
    }

    public int top() {
        return nums.peek();
    }

    public int getMin() {
        return min.peek();
    }
}
```

### Solutions with one stacks

```java
class MinStack {
    long min;
    Stack<Long> stack = new Stack<>();
    
    public void push(int x) {
        if (stack.empty()){
            stack.push(0L);
            min = x;
        }else{
            stack.push(x - min);
            if (x < min){min = x;}
        }
    }

    public void pop() {
        if (!stack.empty()){
            long pop = stack.pop();
            // get the old "min"
            if (pop < 0) min = min - pop;
        }
    }

    public int top() {
        long top = stack.peek();
        if (top > 0){
            return (int) (min + top);
        }else{
            return (int) min;
        }
    }

    public int getMin() {
        return (int) min;
    }
}
```