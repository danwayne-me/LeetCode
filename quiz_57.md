##Quiz#57

*同56非常相似*

给定一组互不重合的区间, 向其中插入一个区间并合并, 输出之后的区间序列

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
    public List<Interval> insert(List<Interval> intervals, Interval newInterval) {
       
    }
}
```

* 优化暴力解:

解法同56, 将新区间插入输入区间序列然后排序, 之后进行合并

```java
class Solution {
    public List<Interval> insert(List<Interval> intervals, Interval newInterval) {
        List<Interval> res = new ArrayList<>();
        if (intervals == null || intervals.size() == 0) {
            res.add(newInterval);
            return res;
        }
        
        intervals.add(newInterval);
        Collections.sort(intervals, new Comparator<Interval>(){
            public int compare(Interval o1, Interval o2) {
                int diff = o1.start - o2.start;
                if (diff == 0) {
                    diff = o1.end - o2.end;
                }
                return diff;
            } 
        });
        
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