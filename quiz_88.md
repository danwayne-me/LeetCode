##Quiz#88

给定两个有序数组nums1, nums2, 将nums2合并入nums1

由于nums1前提保证有足够的空间, 所以**倒着合并!**

```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int i = m - 1, j = n - 1, k = m + n - 1;
        while (i > -1 && j > -1) nums1[k--] = nums1[i] >= nums2[j] ? nums1[i--] : nums2[j--];
        while (j > -1) nums1[k--] = nums2[j--];
    }
}
```