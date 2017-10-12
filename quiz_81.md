##Quiz#81

给定一个升序数组，其中左边一部分被反转并被放到了右边，在这样一个反转数组里查找目标数字, **数组中可能包含重复元素**

```
[4,5,6,7,0,1,2] 中查找5
```

* 二分法解：

不同于通常的二分法， 由于该数组被折叠过，所以二分之后可能存在其中一部分无序，判断二分的条件需要加强为只有目标在有序的那一半才进入，否则进入另一半

```java
class Solution {
    public boolean search(int[] nums, int target) {
        int length = nums.length;
        int start = 0, end = length-1;
        while (start <= end) {
            int mid = (start + end) / 2;
            if (nums[mid] == target) return true;
            if (nums[mid] > nums[end] || nums[mid] > nums[start]) {
                // We would assume the left part is sorted
                if (target < nums[mid] && target >= nums[start]) {
                    end = mid - 1;
                } else {
                    start = mid + 1;
                }
            } else if (nums[mid] < nums[end] || nums[mid] < nums[start]) {
                // We would assume the right part is sorted
                if (target > nums[mid] && target <= nums[end]) {
                    start = mid + 1;
                } else {
                    end = mid - 1;
                }
            } else {
                // nums[mid] == nums[start] == nums[end]
                end--;
            }
        }
        return false;
    }
}
```