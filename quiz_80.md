##Quiz#80

给定一个有序数组，需要保证每个元素至多出现两次，将数组进行调整，把合法数字放到数组前端，同时保证有序，并返回合法的子数组的长度

```
[1,1,1,2,2,3] 返回5，同时将数组前5位调整为[1,2,2,2,3]
```

* 暴力解：

用额外数组保存合法数字，再将其赋值回数组

* 直接赋值解：

从当前数组头部开始标记合法数字，当重复数目小与阈值时就向合法数字部分赋值

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums == null) return 0;
        int length = nums.length;
        if (length < 3) return length;
        int res = 1;
        int count = 1;
        for (int i = 1;i < length;i++) {
            if (nums[i] == nums[i-1]) {
                count++;
            } else {
                count = 1;
            }
            if (count < 3) {
                nums[res++] = nums[i];    
            }
        }
        return res;
    }
}
```