# 剑指 Offer 59 - II. 队列的最大值

<!--创建时间：2020-12-09-->

## 问题描述：

请定义一个队列并实现函数 max_value 得到队列里的最大值，要求函数max_value、push_back 和 pop_front 的均摊时间复杂度都是O(1)。

若队列为空，pop_front 和 max_value 需要返回 -1

**示例 1：**

```java
输入: 
["MaxQueue","push_back","push_back","max_value","pop_front","max_value"]
[[],[1],[2],[],[],[]]
输出: [null,null,null,2,1,2]
```

**示例2：**

```java
输入: 
["MaxQueue","pop_front","max_value"]
[[],[],[]]
输出: [null,-1,-1]
```

## 解题思路：

核心思想：由于较大的数字入队列后，其前面较小的数字出队列时也不会影响此时队列的最大值，所以对于计算最大值而言，前面的较小的数字没有作用。例如有数字[6 3 2 5]，对于5来说，3,2都不会影响最大值，所以3,2,不用记录。可以使用一个辅助的双端队列用于记录最大值。此时辅助队列元素为[6,5]。

当入栈时，正常队列入栈。辅助队列将当前队列尾端小于该入栈元素的元素出列。

当出栈时，正常队列出栈。如果出栈元素与辅助队列头的元素一致，则辅助队列头出列。

例如序列 6 3 2 5， 定义正常队列p， 辅助队列q

//辅助队列的队头元素即为队列的最大值。

p=[6]   q=[6]

p=[6,3] q=[6,3]

p=[6,3,2] q=[6,3,2]

p=[6,3,2,5] q=[6,5] //对于此时的队列，3,2出列不会改变5是队列最大值的事实，所以3,2不用保存在辅助队列中。

## 解题代码：

```java
class MaxQueue {

    private Deque<Integer> max_number;
    private Queue<Integer> q;

    public MaxQueue() {
        max_number = new LinkedList<>();
        q = new LinkedList<>();
    }
    
    public int max_value() {
        if(!max_number.isEmpty())
            return max_number.peekFirst();
        else
            return -1;
    }
    
    public void push_back(int value) {
        q.offer(value);
        while(max_number.peekLast()!=null)
        {
            if(max_number.peekLast()<value)
                max_number.pollLast();
            else
                break;
        }
        max_number.offerLast(value);
    }
    
    public int pop_front() {
        if(q.isEmpty())
            return -1;
        int tmp = q.poll();
        if(tmp==max_number.peekFirst())
            max_number.pollFirst();
        return tmp;
    }
}

/**
 * Your MaxQueue object will be instantiated and called as such:
 * MaxQueue obj = new MaxQueue();
 * int param_1 = obj.max_value();
 * obj.push_back(value);
 * int param_3 = obj.pop_front();
 */
```

