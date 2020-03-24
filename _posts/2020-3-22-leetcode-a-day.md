---
layout: post
title: The Leetcode-A-Day Challenge
---
*To become a leet coder*

During the coronavirus quarantine, I am challenging myself to complete one Topcoder problem each day. Might as well put this free time to good use!

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

# Leetcode Day 2: Reverse Integer
[Link to the Problem](https://leetcode.com/problems/reverse-integer/)

My Solution
```kotlin
class Solution {
    fun reverse(x: Int): Int {
        var num: Long = x.toLong()
        var reverse: Long = 0L
        var digit: Long = 0L
         
        while (num != 0L) {
            // Take digit from end of num
            digit = num % 10L
            num /= 10L
            
            // Add digit to end of reverse
            reverse = reverse * 10L + digit
        }
        
        // Check for overflow / underflow and return
        if (reverse > Int.MAX_VALUE || reverse < Int.MIN_VALUE) {
            return 0
        } else {
            return reverse.toInt()
        }
    }
}
```

Notes
- This problem is all about *anticipating overflow errors.* Reversing an Int can result in a number much larger or smaller than the original. For example:
  - The maximum value of a 32-bit Int is `2147483647` and the minimum is `-2147483648`
  - If the given number is `1111111119`, then it is below this maximum. However, reversing it will give `9111111111` which is *above* the maximum.
  - If the given number is `-1111111119`, then the reverse is `-9111111111` and the same problem applies.
- While I could have checked for overflows after each loop of the calculation, I found it more readable to use Long values for the calculation and to check at the end.
  - My solution was still more memory-efficient than 100% of Kotlin submissions. Nice!
  - If speed was the priority, then it would be more efficient to stop as soon as an overflow occurs to avoid wasting cycles.
- The key to this problem, and to many Leetcode problems, is to *always think about the overflow conditions!*