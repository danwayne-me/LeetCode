## Quiz#56

给定一组区间, 将区间的重合部分合并之后输出

```java
/**
 * Definition for an interval.
 * public class Interval {
 *     int start;
 *     int end;
 *     Interval() { start = 0; end = 0; }
 *     Interval(int s, int e) { start = s; end = e; }
 * }
 */
class Solution {
    public List<Interval> merge(List<Interval> intervals) {
        
    }
}
```

* 暴力解: 

按照题面意思, 将所有输入的区间从左到右进行排序, 然后将排序后的区间列表按照栈的方式每次pop栈顶两个区间, 判断是否可以合并, 将无法合并的左区间加入返回列表, 循环执行该操作直到输入的区间列表为空

```java
class Solution {
    public List<Interval> merge(List<Interval> intervals) {
        if (intervals == null || intervals.size() == 0) {
        	return new ArrayList<Interval>();
        }
        Collections.sort(intervals, new Comparator<Interval>() {
        	@Override
        	public int compare(Interval o1, Interval o2) {
        		// TODO Auto-generated method stub
        		return Integer.signum(o1.start - o2.start);
        	}
		});
        
        List<Interval> res = new ArrayList<>();
        while (intervals.size() > 1) {
        	Interval it1 = intervals.remove(0);
        	Interval it2 = intervals.remove(0);
        	
        	if (it2.start > it1.end) {
        		res.add(it1);
        		intervals.add(0, it2);
        	} else {
        		it1.end = Math.max(it1.end, it2.end);
        		intervals.add(0, it1);
        	}
        }
        if (!intervals.isEmpty()) {
        	res.add(intervals.get(0));
        }
        return res;
    }
}
```

* 优化暴力解: 

由于Interval对象的引用在该对象加入res中之后任然可以被我们得到 我们可以直接修改该对象, 而不用反复的对输入进行插入删除操作

```java
class Solution {
    public List<Interval> merge(List<Interval> intervals) {
        if (intervals == null || intervals.size() == 0) {
        	return new ArrayList<Interval>();
        }
        Collections.sort(intervals, new Comparator<Interval>() {
        	@Override
        	public int compare(Interval o1, Interval o2) {
        		// TODO Auto-generated method stub
        		int diff = o1.start - o2.start;
                if (diff == 0) {
                    diff = o1.end - o2.end;
                }
                return diff;
        	}
		});
        
        List<Interval> res = new ArrayList<>();
        Interval lastAdded = null;       
        for (Interval inter : intervals) {
            if (lastAdded == null || lastAdded.end < inter.start) {
                res.add(inter);
                lastAdded = inter;
            } else {
                lastAdded.end = Math.max(lastAdded.end, inter.end);
            }
        }
        return res;
    }
}
```