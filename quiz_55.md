## Quiz#55

跳格子游戏, 输入一组非负整数, 每个数字代表**最多**可以跳跃的格子数, 初始在最左边, 判断是否可以跳到最右边

例如:

	A = [2,3,1,1,4], return true.

	A = [3,2,1,0,4], return false.
	
* 动态规划解:

**隐藏信息: 由于每个数字代表最多可以跳跃的格子数, 即跳跃格子数可以从一到该数字, 所以可达的格子必定连续, 即如果可以到达最后一个格子, 必然可以到达该数组中的每个格子**

构建辅助数组记录每个格子的可达性, 在可达的格子中, 如果有一个格子的数字大于等于其到最后一个格子的距离, 则返回true, 只要**中间有任何一个格子不可达, 直接返回false**(理由参见隐藏信息)

```java
class Solution {
    public boolean canJump(int[] nums) {
    	if (nums == null || nums.length == 0) {
    		return false;
    	}
    	int length = nums.length;
    	int[] reachable = new int[length];
    	reachable[0] = 1;
    	for (int i = 1;i < length;i++) {
    		for (int j = i - 1;j >= 0;j--) {
    			if (reachable[j] == 1 && nums[j] + j >= i) {
    				reachable[i] = 1;
    				break;
    			}
    		}
    		if (reachable[i] == 0) {
    			return false;
    		}
    	}
    	return true;
    }
}
```

* 可达边界解:

从左边开始跳格子, 对于第i个格子来说, 它能达到的右边界是nums[i] + i, 在右边界左边的所有格子都是可达的, 从左边第一个格子开始, 一次判断每个格子可达的右边界, 记录右边界的最大值, 如果格子的位置超出最大值, 意味着该格子不可达, 根据上述隐藏信息, 直接返回false, 否则返回true

```java
class Solution {
    public boolean canJump(int[] nums) {
    	if (nums == null || nums.length == 0) {
    		return false;
    	}
    	int reachable = 0, length = nums.length;
        for (int i = 0;i < length;i++) {
            if (i > reachable) {
                return false;
            }
            reachable = Math.max(reachable, nums[i] + i);
        }
    	return true;
    }
}
```