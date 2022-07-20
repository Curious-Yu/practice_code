# Grokking-the-Coding-Interview-Patterns-for-Coding-Questions

***

## 1. Pattern: Sliding Window

👉 Maximum Sum Subarray of Size K (easy)

### 53. Maximum Subarray

Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

A subarray is a contiguous part of an array.

Example 1:

Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.

Example 2:

Input: nums = [1]
Output: 1

Example 3:

Input: nums = [5,4,-1,7,8]
Output: 23
 
Constraints:

1 <= nums.length <= 105
-104 <= nums[i] <= 104

```
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxSubArray = function(nums) {
    
    let sum = nums[0];
    let solution = sum;
    
    if (nums.length <= 1){
        return nums;
    }
    
    for (var i=1; i<nums.length; i++){
        
        sum = Math.max(nums[i], nums[i] + sum);
        
        solution = Math.max(solution, sum);

    }
    
    return solution;
    
};
```






👉 Smallest Subarray with a given sum (easy)

### 209. Minimum Size Subarray Sum

Given an array of positive integers nums and a positive integer target, return the minimal length of a contiguous subarray [numsl, numsl+1, ..., numsr-1, numsr] of which the sum is greater than or equal to target. If there is no such subarray, return 0 instead.

 

Example 1:

Input: target = 7, nums = [2,3,1,2,4,3]

Output: 2
Explanation: The subarray [4,3] has the minimal length under the problem constraint.

Example 2:

Input: target = 4, nums = [1,4,4]
Output: 1

Example 3:

Input: target = 11, nums = [1,1,1,1,1,1,1,1]
Output: 0
 

Constraints:

1 <= target <= 109
1 <= nums.length <= 105
1 <= nums[i] <= 104

```
var minSubArrayLen = function(target, nums) {
    
    let sum = 0;
    let subLength = Infinity;
    
    let left = 0;
    
    for (var i=0; i<nums.length; i++){
        sum += nums[i];
        while (sum >= target){
            sum -= nums[left];
            subLength = Math.min(subLength, i-left+1);
            left++;
        }
        
    }
    
    if (subLength === Infinity){
        return 0;
    }
    
    return subLength;
    
};
```

```
/**
 * @param {number} target
 * @param {number[]} nums
 * @return {number}
 */
var minSubArrayLen = function(target, nums) {
    
    
    let subLength = Infinity;
    
    
    let left = 0;
    let right = 1;
    let count = 2;
    
    if (nums[left] >= target){
        return 1;
    }
    
    let sum = nums[left] + nums[right];
    
    while (right < nums.length){
        if (sum < target){
            right++;
            count++;
            sum += nums[right];
        } else {
            sum -= nums[left];      
            subLength = Math.min(subLength, count);
            count--;
            left++;
        }
        
    }
    
    if (subLength === Infinity){
        return 0;
    }
    
    return subLength;
    
    
};
```




👉 Longest Substring with K Distinct Characters (medium)

### 424. Longest Repeating Character Replacement

You are given a string s and an integer k. You can choose any character of the string and change it to any other uppercase English character. You can perform this operation at most k times.

Return the length of the longest substring containing the same letter you can get after performing the above operations.

 

Example 1:

Input: s = "ABAB", k = 2
Output: 4
Explanation: Replace the two 'A's with two 'B's or vice versa.

Example 2:

Input: s = "AABABBA", k = 1
Output: 4
Explanation: Replace the one 'A' in the middle with 'B' and form "AABBBBA".
The substring "BBBB" has the longest repeating letters, which is 4.
 

Constraints:

1 <= s.length <= 105
s consists of only uppercase English letters.
0 <= k <= s.length

```
/**
 * @param {string} s
 * @param {number} k
 * @return {number}
 */
var characterReplacement = function(s, k) {
    
    let frqCount = 0;
    let charCount = 0;
    
    let left = 0;
    let right = 0;
    
    let checkSub = new Map();
    
    while (right < s.length){

        let rSub = s[right];
        
        checkSub.set(rSub, checkSub.get(rSub) + 1 || 1);
        right++;
        charCount++;
        
        frqCount = Math.max(frqCount, checkSub.get(rSub));

        
        if (charCount - frqCount > k){
            
            let lSub = s[left];
            left++;
            charCount--;
            
            checkSub.set(lSub, checkSub.get(lSub) - 1);
            
            if (checkSub.get(lSub) <= 0){
                checkSub.delete(lSub);
            }
        }

    }
        
    return charCount;
};
```

👉 Fruits into Baskets (medium)

### 904. Fruit Into Baskets

You are visiting a farm that has a single row of fruit trees arranged from left to right. The trees are represented by an integer array fruits where fruits[i] is the type of fruit the ith tree produces.

You want to collect as much fruit as possible. However, the owner has some strict rules that you must follow:

You only have two baskets, and each basket can only hold a single type of fruit. There is no limit on the amount of fruit each basket can hold.
Starting from any tree of your choice, you must pick exactly one fruit from every tree (including the start tree) while moving to the right. The picked fruits must fit in one of your baskets.
Once you reach a tree with fruit that cannot fit in your baskets, you must stop.
Given the integer array fruits, return the maximum number of fruits you can pick.

 

Example 1:

Input: fruits = [1,2,1]
Output: 3
Explanation: We can pick from all 3 trees.

Example 2:

Input: fruits = [0,1,2,2]
Output: 3
Explanation: We can pick from trees [1,2,2].
If we had started at the first tree, we would only pick from trees [0,1].

Example 3:

Input: fruits = [1,2,3,2,2]
Output: 4
Explanation: We can pick from trees [2,3,2,2].
If we had started at the first tree, we would only pick from trees [1,2].
 

Constraints:

1 <= fruits.length <= 105
0 <= fruits[i] < fruits.length

```
/**
 * @param {number[]} fruits
 * @return {number}
 */
var totalFruit = function(fruits) {
    
    let basket = new Map();
    
    let left = 0;
    let right = 0;
    
    let max = 0;
    
    while (right < fruits.length){
        let eachFruit = fruits[right];
        basket.set(eachFruit, (basket.get(eachFruit) || 0) + 1);
        right++;
        
        if (basket.size > 2){
            let badFruit = fruits[left];
            
            basket.set(badFruit, (basket.get(badFruit)) - 1);
            if (basket.get(badFruit) <= 0){
                basket.delete(badFruit);
            }
            
            left++;
        }
        
        max = Math.max(max, right - left);
    }
    
    return max;
    
};
```



👉 No-repeat Substring (hard)

### 3. Longest Substring Without Repeating Characters

Given a string s, find the length of the longest substring without repeating characters.

 

Example 1:

Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.

Example 2:

Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.

Example 3:

Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.

```
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLongestSubstring = function(s) {
    
    let subCount = 0;
    let total = 0;
    
    let left = 0;
    let right = 0;
    
    let checkRepeat = new Map();
    
    while (right < s.length){
        if (checkRepeat.has(s[right])){
            checkRepeat.delete(s[left]);
            left++;
            subCount--;
        } else {
            checkRepeat.set(s[right], 1);
            subCount++;
            right++;
        }
        
        total = Math.max(total, subCount);

    }
    
    return total;
    
};
```






👉 Longest Substring with Same Letters after Replacement (hard)

👉 Longest Subarray with Ones after Replacement (hard)

***

## 2. Pattern: Two Pointers

👉 Pair with Target Sum (easy)

👉 Remove Duplicates (easy)

👉 Squaring a Sorted Array (easy)

👉 Triplet Sum to Zero (medium)

👉 Triplet Sum Close to Target (medium)

👉 Triplets with Smaller Sum (medium)

👉 Subarrays with Product Less than a Target (medium)

***

## 3. Pattern: Fast & Slow pointers

👉 LinkedList Cycle (easy)

👉 Middle of the LinkedList (easy)

👉 Start of LinkedList Cycle (medium)

👉 Happy Number (medium) *

***

## 4. Pattern: Merge Intervals

👉 Merge Intervals (medium)

👉 Insert Interval (medium)

👉 Intervals Intersection (medium)

👉 Conflicting Appointments (medium)

***

## 5.Pattern: Cyclic Sort

👉 Cyclic Sort (easy)

👉 Find the Missing Number (easy)

👉 Find all Missing Numbers (easy)

👉 Find the Duplicate Number (easy)

👉 Find all Duplicate Numbers (easy)

***

## 6. Pattern: In-place Reversal of a LinkedList

👉 Reverse a LinkedList (easy)

👉 Reverse a Sub-list (medium)

👉 Reverse every K-element Sub-list (medium)

***

## 7. Pattern: Tree Breadth First Search

👉 Binary Tree Level Order Traversal (easy)

👉 Reverse Level Order Traversal (easy)

👉 Zigzag Traversal (medium)

👉 Level Averages in a Binary Tree (easy)

👉 Minimum Depth of a Binary Tree (easy)

👉 Level Order Successor (easy)

👉 Connect Level Order Siblings (medium)

***

## 8. Pattern: Tree Depth First Search

👉 Binary Tree Path Sum (easy)

👉 All Paths for a Sum (medium)

👉 Sum of Path Numbers (medium)

👉 Path With Given Sequence (medium)

👉 Count Paths for a Sum (medium)

***

## 9. Pattern: Two Heaps

👉 Find the Median of a Number Stream (medium)

👉 Sliding Window Median (hard)

👉 Maximize Capital (hard)

***

## 10. Pattern: Subsets

👉 Subsets (easy)

👉 Subsets With Duplicates (easy)

👉 Permutations (medium)

👉 String Permutations by changing case (medium)

👉 Balanced Parentheses (hard)

👉 Unique Generalized Abbreviations (hard)

***

## 11. Pattern: Modified Binary Search

👉 Order-agnostic Binary Search (easy)

👉 Ceiling of a Number (medium)

👉 Next Letter (medium)

👉 Number Range (medium)

👉 Search in a Sorted Infinite Array (medium)

👉 Minimum Difference Element (medium)

👉 Bitonic Array Maximum (easy)

***

## 12. Pattern: Bitwise XOR

👉 Single Number (easy)

👉 Two Single Numbers (medium)

👉 Complement of Base 10 Number (medium)

***

## 13. Pattern Top 'K' Elements

👉 Top 'K' Numbers (easy)

👉 Kth Smallest Number (easy)

👉 'K' Closest Points to the Origin (easy)

👉 Connect Ropes (easy)

👉 Top 'K' Frequent Numbers (medium)

👉 Frequency Sort (medium)

👉 Kth Largest Number in a Stream (medium)

👉 'K' Closest Numbers (medium)

👉 Maximum Distinct Elements (medium)

👉 Sum of Elements (medium)

👉 Rearrange String (hard)

***

## 14. Pattern: K-way merge

👉 Merge K Sorted Lists (medium)

👉 Kth Smallest Number in M Sorted Lists (Medium)

👉 Kth Smallest Number in a Sorted Matrix (Hard)

👉 Smallest Number Range (Hard)

***

## 15. Pattern : 0/1 Knapsack (Dynamic Programming)

👉 0/1 Knapsack (medium)

👉 Equal Subset Sum Partition (medium)

👉 Subset Sum (medium)

👉 Minimum Subset Sum Difference (hard)

***

## 16. Pattern: Topological Sort (Graph)

👉 Topological Sort (medium)

👉 Tasks Scheduling (medium)

👉 Tasks Scheduling Order (medium)

👉 All Tasks Scheduling Orders (hard)

👉 Alien Dictionary (hard)

***

## 17. Miscellaneous

👉 Kth Smallest Number (hard)

***

[14 Patterns to Ace Any Coding Interview Question](https://hackernoon.com/14-patterns-to-ace-any-coding-interview-question-c5bb3357f6ed)
