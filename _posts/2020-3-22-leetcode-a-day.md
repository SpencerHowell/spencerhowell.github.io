---
layout: post
title: The Leetcode-A-Day Challenge
---
*To become a leet coder*

For a week during the coronavirus quarantine, I am challenging myself to complete one Leetcode problem each day. Might as well put this free time to good use!

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

### Day 2: Reverse Integer
[Link to the problem](https://leetcode.com/problems/reverse-integer/)

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

### Day 3: Palindrome Number
[Link to the problem](https://leetcode.com/problems/palindrome-number/)

My Solution
```kotlin
class Solution {
    fun isPalindrome(x: Int): Boolean {
        return (x.toString() == x.toString().reversed())
    }
}
```

Notes
- This was just a quick one for today!
- I wanted to see if I could solve it in one line - and I did!
- The follow-up challenge is to do it without converting to a string. I'll update here when I get a chance to do so!

### Day 4: String to Integer (atoi)
[Link to the problem](https://leetcode.com/problems/string-to-integer-atoi/)

My Solution
```kotlin
class Solution {
    fun myAtoi(str: String): Int {
        var start = 0 // The starting index of the substring to process
        var end = 0 // The ending index of the substring to process
        var multiplier = 1 // Sets the sign of the result
        
        // Skip whitespace
        while (start != str.length && str.get(start) == ' ') { start++ }
        if (start == str.length) return 0
        
        // Check for plus or minus
        if (str.get(start) == '-') {
            multiplier = -1
            start++
        } else if (str.get(start) == '+') {
            start++ // Skip the plus sign, keep multiplier as 1
        }
        
        // Find the end of the digit sequence
        end = start
        while (end != str.length && str.get(end).isDigit()) { 
            end++ 
        }
        if (end == start) return 0
        
        // Check for overflow / underflow and return
        try {
            return str.substring(start, end).toInt() * multiplier
        }
        catch (e: NumberFormatException) {
            return if (multiplier == 1) Int.MAX_VALUE else Int.MIN_VALUE
        }
    }
}
```

Notes
- While I love features like `filter` and `forEach` in Kotlin, this was one problem where they were not very useful due to the various edge cases.
    - For example, filtering out whitespace seemed like a good idea, but if input string is `1234 5678` the result will be incorrect.
    - If you know a way to use these methods (without an early break) let me know!
- For more control, I ended up using String methods to find the desired substring, and then converting it to an Int.
- This problem gave me a chance to hone my error-catching skills. This helped to simplify the min and max value results.

### Day 5: Add Two Numbers
[Link to the problem](https://leetcode.com/problems/add-two-numbers/)

My Solution
```kotlin
/**
 * Example:
 * var li = ListNode(5)
 * var v = li.`val`
 * Definition for singly-linked list.
 * class ListNode(var `val`: Int) {
 *     var next: ListNode? = null
 * }
 */
class Solution {
    fun addTwoNumbers(l1: ListNode?, l2: ListNode?): ListNode? {
        var listOne : ListNode? = l1
        var listTwo : ListNode? = l3
        var result : ListNode? = null 
        var resultHead : ListNode? = null
        var digit = 0
        var carry = 0
        
        while(listOne != null || listTwo != null || carry != 0) {
            digit = carry 
            
            if (listOne != null) {
                digit += listOne.`val`
                listOne = listOne.next
            }
            if (listTwo != null) {
                digit += listTwo.`val`
                listTwo = listTwo.next
            }
            
            carry = digit / 10
            digit = digit % 10
            if (result == null) {
                result = ListNode(digit)
                resultHead = result
            }  else {
                result.next = ListNode(digit)
                result = result.next
            }
        }
        
        return resultHead 
    }
}
```

Notes:
- This one was a little more involved! The trickiest part for me wasn't the logic, but figuring out how to get Kotlin to play nice with lower-level programming. This is different from what I do with Android development!
- It looks like the problem is actually outdated: the ListNode class is declared with a `var` parameter, which is now no longer supported. I was not sure how to handle this at first. Turns out backticks are required to access the property.
- Another consideration was keeping track of the result: while I needed to access the most recent node of the resulting list, I had to keep a reference to the head of the list available. The head of the list is returned for the final result at the end. Otherwise only the last node will be submitted!
- My result did well on speed; it's faster than 83% of other Kotlin submissions. It also uses less memory than 100% of other Kotlin submissions.

### Day 6: Middle of the Linked List
[Link to the problem](https://leetcode.com/problems/middle-of-the-linked-list/)

My Solution
```kotlin
class Solution {
    fun middleNode(head: ListNode?): ListNode? {
        var count = 0
        var node = head
        
        while (node != null) {
            count++
            node = node?.next
        }
        
        var mid = count / 2
        node = head
        
        for (n in 0 until mid) {
            node = node?.next
        }
        
        return node
    }
}
```

Notes:
- I will admit, I missed a few days of Leetcode in the middle here! I'm definitely still adjusting to quarrantine life.
- This is a simple problem using a singly linked list.
- While it would be nice to only loop over the list once, since it is singly-linked we have to traverse it at least one and a half times: Once to find the total length, and another to return to the middle node.
- This solution was faster than 95.42% of other Kotlin submissions; I'm not exactly sure what others would be doing to make it slower!

### Day 7: Best Time to Buy and Sell Stock II
[Link to the problem](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/)

My Solution
```kotlin
class Solution {
    fun maxProfit(prices: IntArray): Int {
        var profit = 0
        for (i in 0 until (prices.size - 1)) {
            if (prices[i] < prices[i+1]) profit += prices[i+1] - prices[i]
        }
        
        return profit
    }
}
```

Notes:
- The solution to this problem ended up being a lot simpler than I first thought! The key insight here is that to maximize profit, you want to be earning *each and every time the stock price rises*.
    - This means that you always want to purchase in the "valleys" and sell at the "peaks", or at the local minima and maxima.
- While this algorithm means that you are sometimes selling and buying on the same day, when prices continue to rise consecutively, this does not matter because the costs cancel out to zero. The only thing we care about is the maximum possible profit.
- My first thought process was to brute-force it with a weighted graph and Dijkstra's algorithm, but this solution is *much* simpler.

### Conclusion
Well, I have a week's worth of LeetCode, even if it took me a bit longer than a week! However, I do feel like this process was helpful, and definitely plan on continuing the habit of solving LeetCode problems.

I gained a lot of familiarity with primitive lists in Kotlin, and picked up some neat langauge tricks along the way. In addition, I was able to refresh my skills with the content of my Data Structures and Algorithms courses.

I hope you enjoyed this writeup and feel inspired to solve some problems of your own now! Stay tuned to see what else I am up to during this quarrantine.