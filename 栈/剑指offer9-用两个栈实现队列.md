# 剑指offer9-用两个栈实现队列

<!--创建时间：2020-12-09-->

用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )

> 示例
>
> 输入：
> ["CQueue","appendTail","deleteHead","deleteHead"]
> [[],[3],[],[]]
> 输出：[null,null,3,-1]

## 解题思路：

使用两个栈来实现一个队列，当插入操作时，仅在插入栈1，当要出栈时，如果栈2为空，则将栈1的元素全部弹出并压入栈2，如果不为空，则直接弹出栈2元素。注意，如果栈2还有元素一定是pop栈2中的元素，因为在一次将栈1的元素转移到栈2之后，如果栈1之后push了元素，一定要等待之前栈2的元素pop完了才能pop。比如插入1,2,3,4,5之后，执行删除操作，此时栈1为空，栈2为[1,2,3,4]，此时插入6,7.则删除操作时不需要将栈1的转移到栈2，而是直接pop栈2。

## 解题代码：

```java
class CQueue {
    Deque<Integer>s1;
    Deque<Integer>s2;
    public CQueue() {
        s1 = new LinkedList<>();
        s2 = new LinkedList<>();
    }
    
    public void appendTail(int value) {
        s1.push(value);
    }
    
    public int deleteHead() {
        if(s2.isEmpty())
        {
            while(!s1.isEmpty())
            {
                s2.push(s1.pop());
            }
            if(s2.isEmpty())
                return -1;
            else
                return s2.pop();
        }
        else
            return s2.pop();
    }
}

/**
 * Your CQueue object will be instantiated and called as such:
 * CQueue obj = new CQueue();
 * obj.appendTail(value);
 * int param_2 = obj.deleteHead();
 */
```

