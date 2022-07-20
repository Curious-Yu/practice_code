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

👉 Longest Substring with K Distinct Characters (medium)

👉 Fruits into Baskets (medium)

👉 No-repeat Substring (hard)

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
