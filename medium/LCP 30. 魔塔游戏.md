#### [LCP 30. 魔塔游戏](https://leetcode-cn.com/problems/p0NxJO/solution/java-tan-xin-by-feilue-mawl/)




先求数组和
- 如果为负数，怎么移动都到不了最后一个房间
- 如果非负数，那么就肯定能到达最后一个房间

使用优先队列存储所有已经经过的怪物房间（会扣血的房间）

如果到达一个房间后血量 *<= 0*，就取出队列中最小的元素（扣血最多的房间）放到末尾并把血量加回来
- **因为是到达这个房间以后血量才不够的，队列中最小的元素必定小于等于当前房间，也必定能将血量变正，所以只用取出一次**
- **因为数组和大于$0$所以在最后必定会有足够的血量来访问这个扣血的房间，所以取出之后就可以不用管了**

每次执行完之后加上一次操作的次数即可

```java
class Solution {
    public int magicTower(int[] nums) {
        int sum = 0;
        for(int i : nums) sum += i;
        if(sum < 0) return -1;

        int res = 0;
        long health = 1;
        Queue<Integer> min = new PriorityQueue();
        for(int i = 0; i < nums.length; i++){
            if(nums[i] < 0) min.offer(nums[i]);
            health += nums[i];
            if(health > 0) continue;
            
            health -= min.poll();
            res++;
        }

        return res;
    } 
}
```

