# Leetcode: Contiguous Array     :BLOG:Amusing:


---

Contiguous Array  

---

Similar Problems:  
-   Tag: [#subarray](https://code.dennyzhang.com/tag/subarray)

---

Given a binary array, find the maximum length of a contiguous subarray with equal number of 0 and 1.  

Example 1:  

    Input: [0,1]
    Output: 2
    Explanation: [0, 1] is the longest contiguous subarray with equal number of 0 and 1.

Example 2:  

    Input: [0,1,0]
    Output: 2
    Explanation: [0, 1] (or [1, 0]) is a longest contiguous subarray with equal number of 0 and 1.

Note: The length of the given binary array will not exceed 50,000.  

Github: [challenges-leetcode-interesting](https://github.com/DennyZhang/challenges-leetcode-interesting/tree/master/contiguous-array)  

Credits To: [leetcode.com](https://leetcode.com/problems/contiguous-array/description/)  

Leave me comments, if you have better ways to solve.  

---

    ## Blog link: https://code.dennyzhang.com/contiguous-array
    ## Basic Ideas: Get sum of subarray. (For each 1, add 1; For each 0, extract 1)
    ##              And build a hashmap for the fastest position of a given sum.
    ##
    ##       For each item nums[i]:
    ##             If it's 1, find the fastest position k with sum[k] = sum[i] - 1
    ##             If it's 0, find the faster postion k with sum[k] = sum[i] + 1
    ##
    ## Complexity: Time O(n), Space O(n)
    class Solution:
        def findMaxLength(self, nums):
            """
            :type nums: List[int]
            :rtype: int
            """
            length = len(nums)
            sums = [None] * length
            m = {}
            sum_v = 0
            for i in range(0, length):
                if nums[i] == 1:
                    sum_v += 1
                else:
                    sum_v -= 1
                # get the value of sum
                sums[i] = sum_v
                # track the longest position
                if sum_v not in m:
                    m[sum_v] = i
                else:
                    m[sum_v] = max(m[sum_v], i)
            res = 0
            for i in range(0, length):
                sum_v = sums[i]
                if nums[i] == 1:
                    if sum_v - 1 in m:
                        res = max(res, (m[sum_v-1]-i+1))
                else:
                    if sum_v + 1 in m:
                        res = max(res, m[sum_v+1]-i+1)
            return res