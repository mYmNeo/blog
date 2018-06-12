---
title: Meeting Rooms
date: 2016-04-30 09:44:35
tags: 
    - leetcode
    - algorithm
---
>Given an array of meeting time intervals consisting of start and end times `[[s1,e1],[s2,e2],...]` (si < ei), determine if a person could attend all meetings.
>
>For example,
>Given `[[0, 30],[5, 10],[15, 20]]`,
>return `false`.
<!-- more -->
### Analysis:
简单地排序问题,将所有的interval按照开始时间排序,
然后遍历如果当前的interval的结束时间大于下一个interval的开始时间就返回`false`
### Time and space complexity:
排序时间为主要耗时
time: {% math %}\Theta(n\log n) {% endmath %}
### Code:
```cpp
class Solution {
public:
    bool canAttendMeetings(vector<Interval>& intervals) {
        sort(intervals.begin(), intervals.end(), [](const Interval& a, const Interval& b){
            return a.start < b.start;
        });
        
        int size = intervals.size() - 1;
        for (int i = 0; i < size; ++i) {
            if (intervals[i].end > intervals[i + 1].start) {
                return false;
            }
        }
        return true;
    }
};
```