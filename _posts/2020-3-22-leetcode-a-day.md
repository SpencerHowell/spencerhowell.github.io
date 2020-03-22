---
layout: post
title: The Leetcode-A-Day Challenge
---

During the quarantine due to the coronavirus, I am challenging myself to complete one Topcoder problem each day. Might as well put this free time to good use!

I will be completing each problem in the Kotlin language, as I want to continue to become more familiar with its features and best practices.

I also will be focusing on the "Algorithm" problem section, as I believe applying my knowledge of algorithms and data structures will help me become even more knowlegeable in the topic.

### Day 1: Two Sum
[Link to the problem](https://leetcode.com/problems/two-sum/)

My Solution
```kotlin
class Solution {
    fun twoSum(nums: IntArray, target: Int): IntArray {
        
        /* Check every pairing in nums */ 
        for (i in 0 until (nums.size - 1)) {
            for (j in (i + 1) until nums.size) {
               if (nums[i] + nums[j] == target) return intArrayOf(i, j)
            }
        }
        
        /* Default case - it should never get here on a valid problem */
        return intArrayOf(-1, -1)
    }
}
```

Notes
  - This solution uses *less memory than 100% of Kotlin online submissions* for this problem. Nice!
  - Instead of looping through the entire array twice, the inner loop checks only the elements beyond the first element. Addition is commutative, so this does not affect the answer.
  - The outer loop stops before the last element; this last element has already been paired with the rest of the array.
  - Kotlin requires a default return value, which is why the default case is included.
  - This definitely isn't the fastest solution, as those would likely use a HashMap or similar data structure.