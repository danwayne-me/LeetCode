##Quiz#90

给定一个包含重复元素的数组，求出该数组的所有子集

* 回溯法解：

```java
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        Arrays.sort(nums);
        subset(res, new ArrayList<Integer>(), nums, 0);
        return res;
    }
    
    public void subset(List<List<Integer>> res, List<Integer> curAnswer, int[] nums, int start) {
        res.add(new ArrayList<Integer>(curAnswer));
        for (int i = start;i < nums.length;i++) {
            if (i > start && nums[i] == nums[i-1]) continue;
            curAnswer.add(nums[i]);
            subset(res, curAnswer, nums, i+1);
            curAnswer.remove(curAnswer.size() -1);
        }
    }
}
```