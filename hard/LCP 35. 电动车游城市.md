#### [LCP 35. 电动车游城市](https://leetcode-cn.com/problems/DFPeFJ/solution/java-dijkstra-by-feilue-8p14/)

[参考题解](https://leetcode-cn.com/problems/DFPeFJ/solution/dijkstrasuan-fa-qiu-zui-duan-lu-jing-by-usiix/)

首先建图， 存储每个城市相邻的城市和距离 

使用一个二维数组保存结果 *arr\[i][j]* *=* *k*， *i* *=* 所在城市， *j* *=* 剩余电量， *k* *=* 最短时间

用队列来记录每个路径的信息 *\{time, cur, power\}*， *time* *=* 已用时间， *cur* *=* 所在城市， *power* *=* 剩余电量

(**使用优先队列来保证每次优先执行已用时间最少的路径**)



每次只会有两种操作

\- ***\*充一次电\**** - 新时间 *=* 已用时间 *+* 当前城市每单位充电需要时间， 新电量 *=* 剩余电量 + 1

\- ***\*去往下一个城市\**** - 新时间 *=* 已用时间 *+* 去往该需要消耗的时间， 新电量 *=* 剩余电量 *-* 去往该城市需要消耗的电量



```java
class Solution {
    public int electricCarPlan(int[][] paths, int cnt, int start, int end, int[] charge) {
        int n = charge.length;
        
        List<int[]>[] map = new List[n];
        for(int i = 0; i < n; i++) map[i] = new ArrayList();
        for(int[] path : paths){
            map[path[0]].add(new int[]{path[1], path[2]});
            map[path[1]].add(new int[]{path[0], path[2]});
        }

        int[][] res = new int[n][cnt+1];
        for(int[] i : res) Arrays.fill(i, Integer.MAX_VALUE/2);
        res[start][0] = 0;

        Queue<int[]> queue = new PriorityQueue<int[]>((x, y) -> (x[0] - y[0]));
        queue.offer(new int[]{0, start, 0});
        
        while(!queue.isEmpty()){
            int[] arr = queue.poll();
            int time = arr[0];
            int cur = arr[1];
            int power = arr[2];

            if(time > res[cur][power]) continue;
            if(cur == end) return time;

            if(power < cnt){
                int t = time + charge[cur];
                if(t < res[cur][power+1]){
                    res[cur][power+1] = t;
                    queue.offer(new int[]{t, cur, power+1});
                }
            }

            for(int[] path : map[cur]){
                int next = path[0];
                int cost = path[1];
                int t = time + cost;
                int p = power - cost;
                if(p >= 0 && t < res[next][p]){
                    res[next][p] = t;
                    queue.offer(new int[]{t, next, p});
                }
            }

        }

        return -1;
    }
}
```

