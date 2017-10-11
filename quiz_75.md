##Quiz#75

给定一个包含0, 1, 2的数组, 将该数组按升序排序

**由于数组只包含有限种数字, 千万别真的用排序算法去排, 太慢了**

* 统计解( O(2n) ): 

```
统计数组中0, 1, 2的个数, 然后依次把三种数字填入数组
```

* 夹逼解 ( O(n) ): 

由于需要将数组中的三类数字从左到右升序排列, 因此排序后的数组必然可以切为三块, 分别只包含0, 1 和2, 首先分别从左右两边找到初始数组0的右边界和2的左边界, 然后遍历左右边界中间的数组, 遇到0就拓展0的右边界, 遇到2就拓展2的左边界, 这样完成一次遍历之后就可以得到完整的三块数字组成的数组

```java
class Solution {
    public void sortColors(int[] nums) {
        if (nums == null || nums.length == 0) return;
        int length = nums.length;
        int lastRed = -1, firstBlue = length;
        while (lastRed+1 < firstBlue && nums[lastRed+1] == 0)lastRed++;
        while (firstBlue > lastRed+1 && nums[firstBlue-1] == 2)firstBlue--;
        for (int i = lastRed+1;i < firstBlue;) {
            if (nums[i] == 0) {
                if (lastRed == i-1) {
                    lastRed = i;
                    i++;
                } else {
                    lastRed++;
                    if (lastRed >= firstBlue) return;
                    nums[i] = nums[lastRed];
                    nums[lastRed] = 0;
                }
            } else if (nums[i] == 2) {
                firstBlue--;
                if (firstBlue <= lastRed) return;
                nums[i] = nums[firstBlue];
                nums[firstBlue] = 2;
            } else {
                i++;
            }
        }
    }
}
```