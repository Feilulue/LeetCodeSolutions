#### [剑指 Offer II 041. 滑动窗口的平均值](https://leetcode-cn.com/problems/qIsx9U/solution/java-dui-lie-by-feilue-zi0k/)

使用队列模拟滑动窗口



持续记录队列中所有值的合（窗口里值的合）



当队列到达窗口最大size以后将最前面的值取出并减去即可



```java
class MovingAverage {

    Queue<Integer> queue;
    int size;
    double sum;
    
    public MovingAverage(int size) {
        queue = new LinkedList();
        this.size = size;
        sum = 0;
    }
    
    public double next(int val) {
        sum += val;
        if(queue.size() == size) sum -= queue.poll();
        queue.offer(val);
        return sum/queue.size();
    }
}
```

