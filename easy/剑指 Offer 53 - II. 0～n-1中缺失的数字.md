#### [剑指 Offer 53 - II. 0～n-1中缺失的数字](https://leetcode-cn.com/problems/que-shi-de-shu-zi-lcof/solution/java-xor-by-feilue-7cu6/)

- 数组中的所有值以及缺失的数字为 0, 1, 2, .., n-1, n

- 数组长度为n, 那么各个下标为 0, 1, 2, .. , n-1

**将所有下标的值+1即可获得** 1, 2, 3, .., n-1, n



将所有下标的值和数组里出现的值进行异或，最后就只会剩下那个没有出现的数字

（**这种解法可以忽略数组是否排序， 但是需要遍历整个数组**）

```java
class Solution {
    public int missingNumber(int[] nums) {
        int n = nums.length;
        int res = 0;
        for(int i = 0; i < n; i++){
            res ^= nums[i];
            res ^= i + 1;
        }
        return res;
    }
}
```

