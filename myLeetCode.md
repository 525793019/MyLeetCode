# MyLeetCode:
| \#  |Title|Difficulty|Topics|
|:-:  |:-:|:-:|:-:|
|  1  |[**<big id=b1>Two Sum</big>**](#1)|<font color=#22AD22>**E**</font>|Array \| Hash Table|
|  2  |[**<big id=b2>Add Two Numbers</big>**](#2)|<font color=#FFB700>**M**</font>|Linked List \| Math|
|  10 |[**<big id=b10>Regular Expression Matching</big>**](#10)|<font color=#EC043C>**H**</font>|String \| DP \| Backtracking|
|  b  |[**<big id=b></big>**](#n)|<font color=#EC043C>**H**</font>||


## <b id=1>[Two Sum](#b1)</b>
* Given an array of integers, return indices of the two numbers such that they add up to a specific target.

* You may assume that each input would have exactly one solution, and you may not use the same element twice.
#### Example:
```
nums = [2, 7, 11, 15], target = 9
return [0, 1]. 

Because nums[0] + nums[1] = 2 + 7 = 9,
```

#### Thinking:

* 利用Map将遍历后的元素存储起来，通过(key-value)快速查找Map中是否存在与当前值和为目标值的元素。  
时间复杂度：O(n)空间复杂度：O(n)


#### Solution:
```python
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        #记录遍历过的元素
        visited = dict()
        for i,v in enumerate(nums):
            #查找字典中是否存在和为目标值的元素
            if target-v in visited:
                #匹配成功
                return [visited[target-v],i]
            else:
                #匹配失败则将元素存入字典
                visited[v]=i
        return None
```

## <b id=2>[Add Two Numbers](#b2)</b>
* You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.
* You may assume the two numbers do not contain any leading zero, except the number 0 itself.
#### Example:
```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
```
#### Thinking:
* 链表操作问题，注意进位问题即可。
#### Solution:
```c++
#include<iostream>
using namespace std;

struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x){
        val = x;
        next = NULL;
    }
};

class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode * head = new ListNode(0);
        ListNode * n = head;
        int over = 0;

        //循环停止条件为 l1为空 or l2为空 or 没有进位。
        while(l1 || l2 || over){
            n->next = new ListNode(over);
            n = n->next;
            if(l1){
                n->val+=l1->val;
                l1 = l1->next;
            }
            if(l2){
                n->val+=l2->val;
                l2 = l2->next;
            }
            over = n->val/10;
            n->val %= 10;
        }
        return head->next;
    }
};
```
## <b id=10>[Regular Expression Matching](#b10)</b>
* Implement regular expression matching with support for '.' and '*'
* '.' Matches any single character.
* '*' Matches zero or more of the preceding element.
#### Example:
```
isMatch("aa","a") → false
isMatch("aa","aa") → true
isMatch("aaa","aa") → false
isMatch("aa", "a*") → true
isMatch("aa", ".*") → true
isMatch("ab", ".*") → true
isMatch("aab", "c*a*b") → true
```
#### Thinking:
* 动态规划问题，创建动态规划Map，回溯遍历。
1. 查找对应下标的匹配结果，存在返回，反之计算。
2. 确定回溯停止条件。
3. 分情况进行匹配。
4. 返回结果
#### Solution:
```python
class Solution(object):
    def isMatch(self, s, p):
        """
        :type s: str
        :type p: str
        :rtype: bool
        """
        # 存放匹配后的结果
        memo = dict()
        def dp(i, j):
            # i,j分别为s,p的下标。成对存储
            if (i,j) not in memo:
                # 回溯停止条件
                if j==len(p):
                    ans = (i==len(s))
                else:
                    # 当前元素是否匹配
                    match = i<len(s) and (p[j]=='.' or p[j]==s[i])
                    # 不同情况回溯匹配
                    if j+1<len(p) and p[j+1]=='*':
                        # a vs a*   ans赋值表达式很关键!!!
                        ans = (match and dp(i+1,j)) or dp(i,j+2)
                    else:
                        # a vs a|.
                        ans = match and dp(i+1,j+1)
                memo[(i,j)] = ans
            return memo[(i,j)]
        return dp(0,0)
```
## <b id=n>[Title](#b)</b>

#### Example:
```
```
#### Thinking:
#### Solution:
```
```
