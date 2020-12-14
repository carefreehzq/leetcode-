# 剑指 Offer 30. 包含min函数的栈

<!--创建时间：2020-12-09-->

定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。

> 示例：
>
> MinStack minStack = new MinStack();
> minStack.push(-2);
> minStack.push(0);
> minStack.push(-3);
> minStack.min();   --> 返回 -3.
> minStack.pop();
> minStack.top();      --> 返回 0.
> minStack.min();   --> 返回 -2.

## 解题思路：

除了正常的数据栈外，维护一个辅助栈用于保存最小的元素，栈顶元素即为最小的。例如入栈序列[3,5,2,7], 当3入栈后，5就没有必要压入辅助栈，因为此时栈最小的元素就是3，在3出栈之前，5肯定已经出栈了。所以5的压入对栈的最小值没有影响。而2压入时，2变成了最小的元素，所以2需要压入辅助栈。

## 解题代码：

```java
class MinStack {

    /** initialize your data structure here. */
    Stack<Integer>A,B;
    public MinStack() {
        A = new Stack<>();
        B = new Stack<>();
    }
    
    public void push(int x) {
        A.add(x);
        if(B.empty()||B.peek()>=x)
            B.add(x);
    }
    
    public void pop() {
        Integer x=A.pop();
        if(x.equals(B.peek()))
            B.pop();
    }
    
    public int top() {
        return A.peek();
    }
    
    public int min() {
        return B.peek();
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(x);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.min();
 */
```

