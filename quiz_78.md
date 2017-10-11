##Quiz#78

给定n位包含不重复数字的数组, 求出该数组所对应集合的所有子集合

* 递归思想解:

对于该数组的一个子数组来讲，向该子数组新添加一个元素的时候，新数组的所有子集合是原子数组的两倍，其中一半是原有子数组的子集合，另一半是包含了新元素的数组的子集合

```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        res.add(new ArrayList<Integer>());
        if (nums == null || nums.length == 0) {
            return res;
        }
        int length = nums.length;
        for (int i = 0;i < length;i++) {
            List<List<Integer>> tmpList = new ArrayList<>(res);
            for (List<Integer> list : tmpList) {
                List<Integer> newList = new ArrayList<>(list);
                newList.add(nums[i]);
                res.add(newList);
            }
        }
        return res;
    }
}
```