# Overview
Problems, solutions, and solution code are primarily taken from LeetCode solutions or other users, with comments written by me for understanding, along with certain variable name changes for clarity. Links to the problems on LeetCode are included with each question.
## Question Lists
* [Blind Curated 75](https://leetcode.com/list/xoqag3yj/) ([thread link](https://www.teamblind.com/post/New-Year-Gift---Curated-List-of-Top-100-LeetCode-Questions-to-Save-Your-Time-OaM1orEU))
* [LeetCode Patterns](https://seanprashad.com/leetcode-patterns/)
## Notes from Experience
* **Prioritize understanding how to create an algorithm for the problem; thought process > memorization.** If you understand why the solutions work the way they do (and how they would change if the problem was slightly altered), there's probably not much reason why you should have trouble deriving the solution if you see the same/similar question again. This is important because *you definitely should not bank on an exact LC question appearing in an interview,* but you can definitely bank on the same algorithmic patterns appearing in an interview.
* **Information/comprehension builds over time.** IMO, it's better to see all the major problem types/solutions in 1-2 weeks and return to them again later rather than going deep into topics individually; breadth over depth. Even if you don't understand something the first time you see it, returning to it after time passes may make some things click. If you have the time and are just trying to generally get better at LC-style questions, I would prioritize solution concepting (trying to come up with a solution *without* looking at solution, but not coding it) and looking at/understanding the solutions/code of 3-6 questions per hour instead of trying to self-solve 1-2 questions per hour.
* Despite the above point, you should still **look at question types in groups to make seeing common patterns more apparent.**
* Also despite the above, **don't consider a question "solved" until you can do it no hints/solutions in < 30mins.** Note to be mindful with how fresh your knowledge of the specific question is; the idea of this is you have the skill/knowledge to look at a given question, derive what the solution is from the problem statement, and write the code to solve it within 30mins. Anecdotally, people say that if you can solve unseen medium-level questions in <30mins, you're probably good. Be mindful of this also however; recognize that you may be stronger/weaker in certain areas. Also worth noting that even with the "solve a question in < 30mins" constraint, even if you *can't* do that, you still have the knowledge of the question and the patterns; there's no magical border being crossed that signifies you can suddenly "solve the question"; comprehension builds gradually over time, with more time and practice you'll get faster.
* **Don't spend too long trying to solve a question if you can check the solution.** For me, if I can't think of a possible solution within 10 minutes, I just check the answer, try to understand it/the code for 10 minutes, and return another day. If I have a solution in mind, try to implement it for 10-30 minutes; if it looks grim, then I view the solution and return another day.
* **Identify topics, patterns, algorithms, data structures you're weak in, and dig deep into them to understand them.** Check more questions containing your weaknesses and search for patterns/reasoning, read articles/textbook chapters about them.
* **Be able to properly translate the question's solution from thought to working program.** It's possible that I have/had this issue because I did little self-solving at the start; remedy this by just doing/redoing more questions over time without looking at answers.
* **Comment code lines and explain to yourself why it's done the way it is.** If you make yourself explain the solution in a way that's correct and coherent to yourself, you'll likely remember it better. You may also forget the whys over time otherwise.
* **Don't neglect things like variable/function naming, proper spacing, clear/clean code, general proper coding skills, and the thought process.** In an interview setting, these are all important things that the interviewer will be looking for; there may be other things as well dependent on the interviewer/company. The question given is a means to see all of these things, *especially the thought process*.
# Patterns
things that are building blocks of a lot of questions;
## Data Structures
* heap
* stack
* queue
* linkedlist
* hashmap
* tree
* trie (prefix tree)
## Algorithms
* quickselect
* cycle detection
# Question Types
Questions will be organized by their pattern type, if it's not unique; try to organize problems in a given problem type in a way that the knowledge "stacks" onto each other?
## Arrays
### Array Value/Index Tricks
when bounds is something like, `1 <= arr[i] <= len(arr)`, might be an indicator that the solution is related to that; moreso if it asks something like, `Can you solve in O(n) time and O(1) space?`; idea is apparently similar to cycle sort
* LC 287
### k-Sum
* LC 1
* LC 15
### Top K (Order Statistic)
nlogn with sorting; nlogk with heap; n with quickselect; if you have sorting/heap knowledge first 2 are probably easy to get, but quickselect perhaps not as much
___
[Top K problems - Sort, Heap, and QuickSelect](https://leetcode.com/discuss/general-discussion/1088565/Top-K-problems-Sort-Heap-and-QuickSelect)
___

## Graphs/Trees
bfs/dfs; topological sort; union find
### Graphs
### Topological Sort
### Trees
#### Tree Traversal
##### Breadth-First Search (BFS)
sensical for tree level order traversals
##### Depth-First Search (DFS)
##### Level Order Traversal
usually bfs
##### Morris Inorder Traversal
O(n) time, (notably) O(1) space
* LC 99
#### Heap
#### Trie (Prefix Tree)
## Two Pointers
### Sliding Window
## Linked Lists
common themes: dummy nodes, find middle of linked list, reverse linked list, identify/find cycle
## Matrix
## Binary Search
## Backtracking
## DP
## Intervals
## Design
## Bip Manipulation
## Unique/Miscellaneous
### Minimax
___
# []() 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
```

# [1. Two Sum](https://leetcode.com/problems/two-sum/)
## Information
**Category:** Easy

**Patterns:** ?

## Question
Given an array of integers `nums` and an integer `target`, return *indices* of the two numbers such that they *add up* to *`target`*.

You may assume that each input would have ***exactly* one solution**, and you may not use the *same* element twice.

You can return the answer in any order.

**Example 1:**
```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Output: Because nums[0] + nums[1] == 9, we return [0, 1].
```

**Example 2:**
```
Input: nums = [3,2,4], target = 6
Output: [1,2]
```

**Example 3:**
```
Input: nums = [3,3], target = 6
Output: [0,1]
``` 

**Constraints:**
* `2 <= nums.length <= 103`
* `-109 <= nums[i] <= 109`
* `-109 <= target <= 109`
* **Only one valid answer exists.**

## Solutions
* Double `for` loop; return array iterating indices `i` and `j` if `target == (nums[i] + nums[j])`
* For each number in array, insert into hash table (key = number, value = index) and check if hash table contains key `target - nums[i]`; if it does, return `hashtable.get(target - number)` and `i`
## Notes
the goal for two sum is `target = nums[i] + nums[j]`, so you can search for `nums[j]` by applying algebra to the original equation to create `target - nums[i] = nums[j]`. `nums[i]` and `nums[j]` are from the same array, so by storing `target - nums[i]` in a hash table, you can access `nums[j]` in O(1) time, if it exists

## Solution Code
``` py
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        # Initialize dictionary for storing {complement: index}
        complements = {}
        for i, num in enumerate(nums):
            # Since the goal is nums[i] + nums[j] = target, 
            # if nums[j] = target - nums[i] exists, we're done
            complement = target - num
            if complement in complements:
                return [i, complements.get(complement)]

            # Store the current number/index, in case we run into its complement in the future
            complements.setdefault(num, i)
```
# [2. Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        dummy = ListNode()
        current = dummy
        # Use int to store the carry digit if the addition result is >= 10
        carry = 0
        # the lists may have unequal lengths, so null check before getting their values;
        # it's also possible that both lists are null but a carry remains, so check the carry also
        while l1 or l2 or carry:
            val1 = l1.val if l1 else 0
            val2 = l2.val if l2 else 0
            
            # Add both node values and the carry
            val = val1 + val2 + carry
            # If value is >= 10, store the most significant digit in the carry, and mod the value by 10
            carry = val // 10
            val = val % 10
            # Append a new node containing the result to the result linked list
            current.next = ListNode(val)
            
            # Increment nodes
            current = current.next
            l1 = l1.next if l1 else None
            l2 = l2.next if l2 else None
        return dummy.next
```
# [3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        left = 0
        contained_chars = set()
        result = 0
        for right in range(len(s)):
            # If expanding the window to the right introduces a duplicate, 
            # use while loop to shrink the window from the left (remove the character at left, then increment left)
            while s[right] in contained_chars:
                contained_chars.remove(s[left])
                left += 1
            # Add the new character after the window shrinks; doing this beforehand may cause it to be removed unintentionally
            contained_chars.add(s[right])
            # Remember to add 1 to get the actual window size (ex: left, right = 0, 0 is window size 1)
            result = max(result, (right - left) + 1)
        return result
```
# [10. Regular Expression Matching](https://leetcode.com/problems/regular-expression-matching/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def isMatch(self, s: str, p: str) -> bool:
        i, j = 0, 0
        cache = {}
        def check_match(i, j):
            # If a match result has been previously confirmed for both strings at 2 given indicies, return it
            if (i, j) in cache:
                return cache[(i, j)]
            # If both indices for the string and pattern are out of bounds, it's a match
            if i >= len(s) and j >= len(p):
                return True
            # If the pattern is out of bounds but the string isn't, no match
            if j >= len(p):
                return False
            # Logic for determining a match; make sure the string is still in bounds, 
            # as the string can be shorter than the pattern due to *
            match = i < len(s) and (s[i] == p[j] or p[j] == ".")
            # Case to handle *; check if there's a match without the * (increment j by 2), or
            # check if there's a match with the star (increment i by 1)
            if j + 1 < len(p) and p[j + 1] == "*":
                cache[(i, j)] = check_match(i, j + 2) or (match and check_match(i + 1, j))
                return cache[(i, j)]
            # If there's a character match, check for a match for the next characters in the string and pattern
            if match:
                cache[(i, j)] = check_match(i + 1, j + 1)
                return cache[(i, j)]
            # If there's no match and no star, no match
            else:
                cache[(i, j)] = False
                return cache[(i, j)]
        return check_match(0, 0)
```
# [11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def maxArea(self, height: List[int]) -> int:
        left, right = 0, len(height) - 1
        max_water = 0
        while left < right:
            max_water = max(max_water, min(height[left], height[right]) * (right - left))
            if height[left] < height[right]:
                left += 1
            else:
                right -= 1
        return max_water
```
# [15. 3Sum](https://leetcode.com/problems/3sum/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        # Sort the array to make finding combinations faster; consider implementing no sort solutiotn also?
        nums.sort()
        result = []
        
        for i, num in enumerate(nums):
            # Because array is sorted and combinations must be unique, 
            # if the current number is the same as the previous number, it will yield the same results; skip
            if i != 0 and nums[i - 1] == nums[i]:
                continue
            # Use sorted two sum algorithm to find the remaining 2 numbers
            left, right = i + 1, len(nums) - 1
            while left < right:
                candidate = num + nums[left] + nums[right]
                if candidate > 0:
                    right -= 1
                elif candidate < 0:
                    left += 1
                else:
                    result.append([num, nums[left], nums[right]])
                    left += 1
                    # Since array is sorted and combinations must be unique, continuously increment until 
                    # next number isn't the same as the current number
                    while nums[left] == nums[left - 1] and left < right:
                        left += 1
        return result
```
# [17. Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        # Need to hardcode these to create the combinations
        number_to_letters = {
            "2": "abc",
            "3": "def",
            "4": "ghi",
            "5": "jkl",
            "6": "mno",
            "7": "pqrs",
            "8": "tuv",
            "9": "wxyz" 
        }
        result = []
        
        def create_combinations(i, current_string):
            # If the current string is as long as the digits string, done this path; 
            # add the string to the result list and return (start going back)
            if len(current_string) == len(digits):
                result.append(current_string)
                return
            # For every possible character at the current digit, try combinations with it 
            # (recurse on next index with current character included in current_string)
            for char in number_to_letters[digits[i]]:
                create_combinations(i+1, current_string + char)
        if digits:
            create_combinations(0, "")
        return result
```
# 19. Remove Nth Node From End of List
## Information
## Question
## Solutions
* 2 pass approach; loop once to find length of the list, loop again to remove nth element; O(2L) = O(L) time (L = list length) since 2 consecutive loops, O(1) space
* 1 pass approach; 2 pointers, where one pointer is n iterations ahead of the other; once the front pointer reaches the end, remove valule of the back pointer; O(L) time since 1 loop, O(1) space
## Notes
## Solution Code
``` py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        # Need to return the head, so use dummy.next as a reference to head;
        # whenever you need to return the linked list, use dummy.next as a reference to it, 
        # and work with other variables for the algorithm
        dummy = ListNode(0, head)
        # Singly-linked lists can only see ahead of them; need to make sure that 
        # the node you stop on is the node before the one to be removed
        remove_next_node = dummy
        # Use a second node that's n steps ahead of the node to remove;
        # it's set to dummy.next and not dummy because of remove_next_node removing the node after it,
        # not the node that it actually is
        n_ahead_node = dummy.next
        for _ in range(n):
            n_ahead_node = n_ahead_node.next
        # Increment both nodes, searching for the end of the list
        while n_ahead_node:
            remove_next_node = remove_next_node.next
            n_ahead_node = n_ahead_node.next
        # Assign the next node of the node before the node to remove the value of the node to remove's next node
        remove_next_node.next = remove_next_node.next.next
        return dummy.next
```
# [20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        # Map closing parentheses to their corresponding opening parentheses; 
        # makes it easier to determine parenthesis type when parsing the string
        parenthesis_mapping = {")": "(", "}": "{", "]": "["}
        
        # Iterate through string characters
        for char in s:
            # If the character is a closing parenthesis, pop the most recent open parenthesis from the stack, and 
            # check if the parenthesis types match up; if they do, continue; if they don't, return false
            if char in parenthesis_mapping:
                top = stack.pop() if stack else '#'
                if parenthesis_mapping[char] != top:
                    return False
            # If the character is an opening parenthesis, push it onto the stack to check for closure later
            else:
                stack.append(char)
                
        # If stack is empty, all matches were successful; return true. Else, return false 
        # (remaining open parentheses exist)
        if not stack:
            return True
        return False
```
# [21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        # Used for keeping a reference to the first ListNode (dummy.next)
        dummy = ListNode()
        # The value of tail will change to represent the end of thte list; starts at dummy
        tail = dummy
        while l1 and l2:
            if l1.val <  l2.val:
                tail.next = l1
                l1 = l1.next
            else:
                tail.next = l2
                l2 = l2.next
            tail = tail.next
        # One list will run out of elements first; when this happens, 
        # check which one it was and add the rest of that list to the tail
        if l1:
            tail.next = l1
        elif l2:
            tail.next = l2
        return dummy.next
```
# [22. Generate Parentheses](https://leetcode.com/problems/generate-parentheses/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        current_combination = []
        result = []
        def create_combinations(num_open, num_closed):
            # If all opens and closes have been used, add the current combination and return (go back)
            if num_open == num_closed == n:
                result.append("".join(current_combination))
                return
            # If opens can still be used: add one, try combinations with it, then remove it
            if num_open < n:
                current_combination.append("(")
                create_combinations(num_open + 1, num_closed)
                current_combination.pop()
            # If closes can still be used: add one, try combinations with it, then remove it
            if num_closed < num_open:
                current_combination.append(")")
                create_combinations(num_open, num_closed + 1)
                current_combination.pop()
        # Run all possible combinations and return the result
        create_combinations(0, 0)
        return result
```
# [23. Merge k Sorted Lists]()
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeKLists(self, lists: List[ListNode]) -> ListNode:
        # Edge case for k == 0
        if not lists or len(lists) == 0:
            return None
        # While the number of lists is greater than 1, repeatedly merge the lists in groups of 2
        while len(lists) > 1:
            merged_lists = []
            # Since the merging creates a new array, increment by 2 to the same list being merged twice
            for i in range(0, len(lists), 2):
                list_1 = lists[i]
                # If there is an odd number of lists, the second list will be null
                list_2 = lists[i + 1] if (i + 1) < len(lists) else None
                merged_lists.append(self.merge_lists(list_1, list_2))
            lists = merged_lists
        # At the end, there will only be one list in the array, as everything else was merged together
        return lists[0]
    
    # Use merge two sorted lists algorithm
    def merge_lists(self, l1, l2):
        dummy = ListNode()
        tail = dummy
        while l1 and l2:
            if l1.val <  l2.val:
                tail.next = l1
                l1 = l1.next
            else:
                tail.next = l2
                l2 = l2.next
            tail = tail.next
        if l1:
            tail.next = l1
        elif l2:
            tail.next = l2
        return dummy.next
```
# [24. Swap Nodes in Pairs](https://leetcode.com/problems/swap-nodes-in-pairs/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def swapPairs(self, head: ListNode) -> ListNode:
        dummy = ListNode(0, head)
        previous_node = dummy
        current_node = head
        # Check if there's a pair of nodes first; if there isn't, don't swap anything
        while current_node and current_node.next:
            # Store the next node and the first node of the next pair, as to not lose references
            next_pair_first = current_node.next.next
            next_node = current_node.next
            
            # Reverse the next node to point to the current node, 
            # set the previous node to point to the next node,
            # and set the current node to point to the next pair's first node
            next_node.next = current_node
            previous_node.next = next_node
            current_node.next = next_pair_first
            
            # Increment the previous node and current node
            previous_node = current_node
            current_node = next_pair_first
        return dummy.next
```
# [25. Reverse Nodes in k-Group](https://leetcode.com/problems/reverse-nodes-in-k-group/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseKGroup(self, head: ListNode, k: int) -> ListNode:
        dummy = ListNode(0, head)
        previous_group_last = dummy
        
        # TODO: understanding not full yet; return
        # Find the kth element, then reverse LL until you approach kth element's next (swap kth, stop here)
        while True:
            # Search ahead to get the relative kth node, if it exists; if not, don't swap and break
            kth_node = self.get_kth_node(previous_group_last, k)
            if not kth_node:
                break
            next_group_first = kth_node.next
            previous_node = kth_node.next
            current_node = previous_group_last.next
            
            # Reverse the k-sized linked list group until you approach the end (next_group_first)
            while current_node != next_group_first:
                next_node = current_node.next
                current_node.next = previous_node
                previous_node = current_node
                current_node = next_node
                
            # After swapping, kth element is at the start, 
            # and the first element is at the end (previous_group_last.next)
            temp = previous_group_last.next
            previous_group_last.next = kth_node
            previous_group_last = temp
            
        return dummy.next
    
    def get_kth_node(self, current_node, k):
        while current_node and k > 0:
            current_node = current_node.next
            k -= 1
        return current_node
```
# [30. Substring with Concatenation of All Words](https://leetcode.com/problems/substring-with-concatenation-of-all-words/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
```
# [33. Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left, right = 0, len(nums) - 1
        while left <= right:
            # Integer division to get the middle of the array
            mid = (left + right) // 2
            # If the middle is the target, return it
            if nums[mid] == target:
                return mid
            # If the middle number is greater than the leftmost element, left side is normal; check left side
            if nums[mid] >= nums[left]:
                # If the target's value is between the leftmost element and mid, search left side
                # TODO: why check target < nums[mid]?
                if target >= nums[left] and target < nums[mid]:
                    right = mid - 1
                else:
                    left = mid + 1
            # If the leftmost element is greater than the middle number, left side is rotated; check right side
            else:
                if target <= nums[right] and target > nums[mid]:
                    left = mid + 1
                else:
                    right = mid - 1
        return -1
```
# [41. First Missing Positive](https://leetcode.com/problems/first-missing-positive/submissions/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    # "Reduce" the problem to a 1 <= nums[i] <= n "indices as markers" trick 
    # (the one present in "Find All Duplicates in an Array" and "Find All Numbers Disappeared in an Array") by
    # checking if 1 is present; if it is, then consider the fact that any value that's negative, 0, or
    # greater than the length of the array can be discarded/ignored and replaced with a 1, since 1 won't be
    # the first missing positive (since it was already checked); after, go through the array and use indices as markers, 
    # then check every index to see if it's positive; first positive index is the result, and if all are negative, 
    # result is len(nums) + 1
    # 
    # Note: positive values that are greater than the length don't need to be changed, but their values need to be ignored
    # during the marking process (since index would be out of bounds)
    def firstMissingPositive(self, nums: List[int]) -> int:
        n = len(nums)
        # Explicitly check for 1 so it can be used as a fodder value
        if 1 not in nums:
            return 1
        
        # Set any zeroes/negatives/numbers above array length to 1
        for i in range(n):
            if nums[i] <= 0 or nums[i] > n:
                nums[i] = 1
        
        # If the value at an index of num - 1 is not already negative, negate it as a mark for num's value being present
        for num in nums:
            if nums[abs(num) - 1] > 0:
                nums[abs(num) - 1] *= -1
        
        # Iterate from 1 to n to check for positive values; first positive value is the first missing positive
        for i in range(1, n + 1):
            if nums[i - 1] > 0:
                return i
        # If all numbers were negative, first missing positive is array length + 1
        return n + 1
```
# [42. Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    # The water at a current tile = min(max_left_side, max_right_side) - tile_height.
    # Since taking the min, consider that the higher value doesn't actually matter; 
    # only the min value and current tile's height does, which is the basis for 2 pointer approach
    def trap(self, height: List[int]) -> int:
        left, right = 0, len(height) - 1
        result = 0
        # Track the current known max for left and right sides for water storage calculation
        current_left_max, current_right_max = 0, 0
        while left < right:
            # If the current value is greater than the max, set it to the max
            if height[left] > current_left_max:
                    current_left_max = height[left]
            if height[right] > current_right_max:
                current_right_max = height[right]
            
            # Add the lesser side's tile's value to result and move the pointer of that side
            # (calculate current tile's value with max - current height)
            if current_left_max < current_right_max:
                result += current_left_max - height[left]
                left += 1
            else:
                result += current_right_max - height[right]
                right -= 1
        return result
```
# [46. Permutations](https://leetcode.com/problems/permutations/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# This is actually the solution for Permutations II, but the exact same code works; normally, 
# you would just pop numbers from nums and append it to current_permutation, recurse, 
# then push it back onto nums, but that method doesn't work if there's duplicates?
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        results = []
        current_permutation = []
        # Fill a dict with the total number counts for every number in nums
        num_counts = { num: 0 for num in nums }
        for num in nums:
            num_counts[num] += 1
            
        def generate_permutations():
            # If the length of the current permutation = length of nums, add it to results and return (go back)
            if len(current_permutation) == len(nums):
                results.append(current_permutation.copy())
                return
            # Loop through all numbers; if they have counts remaining, try combinations with them
            for num in num_counts:
                if num_counts[num] > 0:
                    current_permutation.append(num)
                    num_counts[num] -= 1
                    generate_permutations()
                    num_counts[num] += 1
                    current_permutation.pop()
        
        generate_permutations()
        return results
```
# [47. Permutations II](https://leetcode.com/problems/permutations-ii/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def permuteUnique(self, nums: List[int]) -> List[List[int]]:
        results = []
        current_permutation = []
        # Fill a dict with the total number counts for every number in nums
        num_counts = { num: 0 for num in nums }
        for num in nums:
            num_counts[num] += 1
            
        def generate_permutations():
            # If the length of the current permutation = length of nums, add it to results and return (go back)
            if len(current_permutation) == len(nums):
                results.append(current_permutation.copy())
                return
            # Loop through all numbers; if they have counts remaining, try combinations with them
            for num in num_counts:
                if num_counts[num] > 0:
                    current_permutation.append(num)
                    num_counts[num] -= 1
                    generate_permutations()
                    num_counts[num] += 1
                    current_permutation.pop()
        
        generate_permutations()
        return results
```
# [48. Rotate Image](https://leetcode.com/problems/rotate-image/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        row_start, row_end = 0, len(matrix)
        col_start, col_end = 0, len(matrix[0])
        while row_start < row_end and col_start < col_end:
            offset = 0
            # TODO: explain this, and the reason why it's not offset < len(matrix) - 1
            while offset < ((row_end - 1) - row_start):
                # Store top left in temp variable
                temp = matrix[row_start][col_start + offset]
                # Move bottom left to top left
                matrix[row_start][col_start + offset] = matrix[(row_end - 1) - offset][col_start]
                # Move bottom right to bottom left
                matrix[(row_end - 1) - offset][col_start] = matrix[row_end - 1][(col_end - 1) - offset]
                # Move top right to bottom right
                matrix[row_end - 1][(col_end - 1) - offset] = matrix[row_start + offset][(col_end - 1)]
                # Move temp (top left) to top right
                matrix[row_start + offset][col_end - 1] = temp
                # Increment the offset so different elements are rotated on the next round
                offset += 1
            # Shrink the size of the matrix portion being swapped
            row_start += 1
            row_end -= 1
            col_start += 1
            col_end -= 1
```
# [49. Group Anagrams](https://leetcode.com/problems/group-anagrams/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        # Use defaultdict(list) here instead of {}, so keys that don't exist initialize as empty lists
        result = defaultdict(list)
        
        for string in strs:
            # Initialize array of 0's size 26
            char_count = [0] * 26
            for char in string:
                # characters start at 'a', so char - a can be used as an offset 
                # (a - a = 0, b - a = 1, ...)
                char_count[ord(char) - ord('a')] += 1
            # The string's letter count is used as the dictionary key, 
            # so all strings with the same letter count (anagrams) are grouped
            result[tuple(char_count)].append(string)
        # Return result.values() here for the list of anagram strings;
        # returning result would give a list of the keys (the tuples) instead of the values (the string lists)
        return result.values()
```
# [51. N-Queens](https://leetcode.com/problems/n-queens/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def solveNQueens(self, n: int) -> List[List[str]]:
        # Track the columns, diagonals, and anti-diagonals with queens in them;
        # TODO: diagonals store what? why 2 * n - 1? 
        cols = [0] * n
        diagonals = [0] * (2 * n-1)
        anti_diagonals = [0] * (2 * n-1)
        queen_placements = set()
        
        result = []
        
        def generate_solutions(row):
            # If all rows are filled with queens, append to result as a valid solution
            if row >= n:
                append_solution()
                return
            for col in range(n):
                if check_valid(row, col):
                    # place queen
                    queen_placements.add((row, col))
                    cols[col] = 1
                    diagonals[row - col] = 1
                    anti_diagonals[row + col] = 1
                    generate_solutions(row + 1)
                    # remove queen
                    queen_placements.remove((row, col))
                    cols[col] = 0
                    diagonals[row - col] = 0
                    anti_diagonals[row + col] = 0
        
        def check_valid(row, col):
            if cols[col] or diagonals[row - col] or anti_diagonals[row + col]:
                return False
            return True
        
        def append_solution():
            solution = []
            for _, col in sorted(queen_placements):
                solution.append('.' * col + 'Q' + '.' * (n - col - 1))
            result.append(solution)
            return
        
        generate_solutions(0)
        return result
```
# [53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        # Since array is guaranteed to be at least size 1, set known max to lowest possible value;
        # it'll be overwritten once the loop starts.
        # If empty arrays were possible, would need an edge case check
        known_max_sum = float('-inf')
        current_sum = 0
        for num in nums:
            # If the current sum is negative, it should be ignored; reset current_sum to do this
            if current_sum < 0:
                current_sum = 0
            current_sum += num
            # The known max will either be itself, or current sum + current number
            known_max_sum = max(known_max_sum, current_sum)
        return known_max_sum
```
# [54. Spiral Matrix](https://leetcode.com/problems/spiral-matrix/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        output = []
        # Get the start/end ranges for unvisited rows/columns; 
        # these will change as rows/columns are visited
        row_start, row_end = 0, len(matrix)
        col_start, col_end = 0, len(matrix[0])
        
        while row_start < row_end and col_start < col_end:
            # Collect all elements in the topmost row
            for col in range(col_start, col_end):
                output.append(matrix[row_start][col])
            # The entire topmost row has been obtained; increment row_start by 1 
            # to make the second row the new topmost row (to prevent re-visiting)
            row_start += 1
            
            # Collect all elements in the rightmost column
            for row in range(row_start, row_end):
                output.append(matrix[row][col_end - 1])
            # Decrement col_end by 1 to prevent re-visiting
            col_end -= 1
            
            # Check here to ensure the loop condition is still true, 
            # as row_start and col_end values have changed inside the loop
            if not (row_start < row_end and col_start < col_end):
                break
            
            # Collect all elements in the bottommost row, going backwards
            for col in range(col_end - 1, col_start - 1, -1):
                output.append(matrix[row_end - 1][col])
            row_end -= 1
            
            # Collect all elements in the leftmost column, going backwards
            for row in range(row_end - 1, row_start - 1, -1):
                output.append(matrix[row][col_start])
            col_start += 1
        return output
```
# [55. Jump Game](https://leetcode.com/problems/jump-game/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        # Only need to check if you can get to the last valid position; starts at the end
        last_position = len(nums) - 1
        for i in range(len(nums) - 1, -1, -1):
            # In order to jump from index i to the last valid position, the current index + its jump distance
            # must be >= the index of the last valid position
            print(i, nums[i], last_position)
            if i + nums[i] >= last_position:
                last_position = i
        # If the last valid position is 0, can reach the end; return true. Else, return false
        if last_position == 0:
            return True
        return False
```
# [56. Merge Intervals](https://leetcode.com/problems/merge-intervals/)
## Information
## Question
## Solutions
* sort array, then loop thru each element: check if current.end > next.start; if true, merge (something like change current.end to next.end, dunno specifics)
## Notes
## Solution Code
``` py
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        # Sort the intervals by start, so overlaps can easily be found
        intervals.sort(key = lambda i : i[0])
        # Start with the first interval inside by default, 
        # so it can be checked on first iteration of the for loop
        merged_intervals = [intervals[0]]
        # Remember to start at the second element, since first element is inserted
        for start_interval, end_interval in intervals[1:]:
            # If the next interval's start time is less than the latest interval's end time, merge the intervals 
            # (done by setting the latest interval's end time to the max of both intervals' end times);
            # else, append the next interval to the merged interval list
            if merged_intervals[-1][1] >= start_interval:
                merged_intervals[-1][1] = max(merged_intervals[-1][1], end_interval)
            else:
                merged_intervals.append([start_interval, end_interval])
        return merged_intervals
```
# [62. Unique Paths](https://leetcode.com/problems/unique-paths/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        # Base case: tiles on the topmost/leftmost only have 1 path to reach, since can only move right/down
        # (out of bounds considered as 0)
        dp = [[1] * n for _ in range(m)]
        # Ignore the first row/col since it's already known to be 1
        for col in range(1, m):
            for row in range(1, n):
                # The number of paths to a given tile is equal to the number of paths of the tile above/left of it
                dp[col][row] = dp[col - 1][row] + dp[col][row - 1]
        return dp[m - 1][n - 1]
```
# [70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def climbStairs(self, n: int) -> int:
        # ways[last] = ways[last - 1] + ways[last - 2]
        # ways[first] = 1
        # ways[first+1] = 2 (reaching step 2)
        if n == 1:
            return 1
        dp = [0] * (n + 1)
        
        # One distinct way to reach step 1, two distinct ways to reach step 2
        dp[1] = 1
        dp[2] = 2
        for i in range(3, n + 1):
            # Reaching step i is # combinations of the previous step + combinations of 2 steps back
            dp[i] = dp[i - 1] + dp[i - 2]
        # Return the # of combinations for the nth step
        return dp[n]
```
# [73. Set Matrix Zeroes](https://leetcode.com/problems/set-matrix-zeroes/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def setZeroes(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        # Use a boolean variable to act as a 0-marker for the columns, since they would overlap and become impossible to differentiate;
        # can pick either row or column, it shouldn't matter
        is_column_zero = False
        
        rows, cols = len(matrix), len(matrix[0])
        for row in range(rows):
            for col in range(cols):
                # If an element is 0, mark the first element of the row/column it's in as 0; this is fine because 
                # those elements should have been checked already
                if matrix[row][col] == 0:
                    matrix[0][col] = 0
                    # TODO: explain this lol
                    if row > 0:
                        matrix[row][0] = 0
                    else:
                        is_column_zero = True
        # Scan the matrix again (except first row/column, special case); if the first element of the row it's part of is 0 or 
        # first element of the column it's part of is 0, set to 0
        for row in range(1, rows):
            for col in range(1, cols):
                if matrix[0][col] == 0 or matrix[row][0] == 0:
                    matrix[row][col] = 0
        
        # Use the top-left element and boolean variable to individually zero out the first row/column
        if matrix[0][0] == 0:
            for row in range(rows):
                matrix[row][0] = 0
        if is_column_zero:
            for col in range(cols):
                matrix[0][col] = 0
```
# [74. Search a 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        rows, cols = len(matrix), len(matrix[0])
        
        # Consider the matrix as a 1D array by considering the end as length of rows * cols
        left, right = 0, rows * cols - 1   
        while left <= right:
            mid = left + (right - left) // 2
            # To get the row, divide by the number of cols; since each row is length cols, 
            # the integer you land on will be the row number
            row = mid // cols
            # To get the column, mod by cols to get the col number
            col = mid % cols
            # After this, apply regular binary search
            if matrix[row][col] == target:
                return True
            if matrix[row][col] > target:
                right = mid - 1
            else:
                left = mid + 1
        return False
```
# [76. Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# TODO: commenting not done yet
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        have_chars, need_chars = {}, {}
        # Populate needed_chars with the character counts of t
        for char in t:
            need_chars[char] = need_chars.get(char, 0) + 1
        # Track the number of distinct letter counts that you currently have, 
        # and distinct letter counts that need to be met
        have_count, need_count = 0, len(need_chars)
        # Track the start/end indices of the result substring for returning, and the length of it
        result_substring, result_length = [-1, -1], float("inf")
        left = 0
        for right in range(len(s)):
            char = s[right]
            have_chars[char] = have_chars.get(char, 0) + 1
            
            if char in need_chars and have_chars[char] == need_chars[char]:
                have_count += 1
            # If all the 
            while have_count == need_count:
                current_length = right - left + 1
                if current_length < result_length:
                    result_substring = [left, right]
                    result_length = current_length
                have_chars[s[left]] -= 1
                if s[left] in need_chars and have_chars[s[left]] < need_chars[s[left]]:
                    have_count -= 1
                left += 1
        if result_length == float("inf"):
            return ""
        return s[result_substring[0]:result_substring[1] + 1]
```
# [77. Combinations](https://leetcode.com/problems/combinations/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def combine(self, n: int, k: int) -> List[List[int]]:
        result = []
        current_combination = []
        def generate_combinations(i):
            if len(current_combination) >= k:
                result.append(current_combination.copy())
                return
            # Iterate through all numbers from the starting number to the max number; try combinations with them, then pop
            for num in range(i, n + 1):
                current_combination.append(num)
                generate_combinations(num + 1)
                current_combination.pop()
        generate_combinations(1)
        return result
```
# [78. Subsets](https://leetcode.com/problems/subsets/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        result = []
        current_subset = []
        def generate_subsets(i):
            # If the current index is out of bounds, finished the permutation; append the current subset result and go back
            if i >= len(nums):
                result.append(current_subset.copy())
                return
            # Try all combinations including the number at this index
            current_subset.append(nums[i])
            generate_subsets(i + 1)
            # Try all combinations without including the number at this index
            current_subset.pop()
            generate_subsets(i + 1)
        generate_subsets(0)
        return result
```
# [81. Search in Rotated Sorted Array II](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    # Solution is the same as "Search in Rotated Sorted Array", but incrementing/decrementing the search space if
    # indices next to the borders are duplicates
    def search(self, nums: List[int], target: int) -> bool:
        left, right = 0, len(nums) - 1
        while left <= right:
            # While the bounds don't cross and the second element is the same as the first, increment left bound
            while left < right and nums[left] == nums[left + 1]:
                left += 1
            # While the bounds don't cross and the second last element is the same as the last, decrement right bound
            while left < right and nums[right] == nums[right - 1]:
                right -= 1
                
            mid = (left + right) // 2
            if nums[mid] == target:
                return True
            if nums[mid] >= nums[left]:
                if target >= nums[left] and target < nums[mid]:
                    right = mid - 1
                else:
                    left = mid + 1
            else:
                if target <= nums[right] and target > nums[mid]:
                    left = mid + 1
                else:
                    right = mid - 1
        return False
```
# [82. Remove Duplicates from Sorted List II](https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def deleteDuplicates(self, head: ListNode) -> ListNode:
        # Use dummy node to maintain access to head of the list, in case the head is deleted
        dummy = ListNode(0, head)
        prev_node, current_node = dummy, dummy.next
        
        while current_node:
            # If the current node has the same value as the next node, continuously increment the current node
            # until the end of the duplicates is reached
            if current_node.next and current_node.val == current_node.next.val:
                while current_node.next and current_node.val == current_node.next.val:
                    current_node = current_node.next
                # After reaching the end, set the previous node's pointer to the current node's next pointer 
                # to remove all references to the duplicate values
                prev_node.next = current_node.next
            # If not a duplicate, increment the previous node
            else:
                prev_node = prev_node.next
            # Increment thet current node to continue searching
            current_node = current_node.next
        return dummy.next
```
# [83. Remove Duplicates from Sorted List](https://leetcode.com/problems/remove-duplicates-from-sorted-list/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def deleteDuplicates(self, head: ListNode) -> ListNode:
        current_node = head
        while current_node and current_node.next:
            # If the next node's value is the same as the current node's value, remove the next node 
            # by setting the current node's next node to the next node's next node (deleting ref to next node).
            # The if statement will continuously run and not increment while there's duplicates due to the if/else
            if current_node.val == current_node.next.val:
                current_node.next = current_node.next.next
            # If different value, increment current node
            else:
                current_node = current_node.next
        return head
```
# [84. Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def largestRectangleArea(self, heights: List[int]) -> int:
        max_area = 0
        # Store the histogram columns in a stack of its starting index and height
        stack = []
        
        for i, current_height in enumerate(heights):
            # Set the starting index to the current index
            start_index = i
            # Continuously check if the top of the stack is greater than the current column; 
            # if it is, the max area it can contribute can't get higher due to the lower height column,
            # so calculate its max height and pop it
            while stack and stack[-1][1] > current_height:
                index, height = stack.pop()
                # The max height is either the current max height, or
                # the height of the popped column * the difference of the current index and the popped column's start index
                max_area = max(max_area, height * (i - index))
                # The actual starting index of the current column can be moved back, 
                # considered as the start index of the popped column
                start_index = index
            # Append the current column to the stack
            stack.append((start_index, current_height))
        # If any columns remain at the end, calculate their max heights
        for i, height in stack:
            max_area = max(max_area, height * (len(heights) - i))
        return max_area
```
# [86. Partition List](https://leetcode.com/problems/partition-list/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def partition(self, head: ListNode, x: int) -> ListNode:
        # Create two lists; lesser holds values < x, greater holds values >= x
        lesser_dummy, greater_dummy = ListNode(), ListNode()
        lesser_tail, greater_tail = lesser_dummy, greater_dummy
        
        # Iterate through all the nodes, assigning the values to the lesser or greater list
        while head:
            if head.val < x:
                lesser_tail.next = head
                lesser_tail = lesser_tail.next
            else:
                greater_tail.next = head
                greater_tail = greater_tail.next
            head = head.next
        
        # Attach the end of the lesser list to the start of the greater list, and set the end of the greater list to null
        lesser_tail.next = greater_dummy.next
        greater_tail.next = None
        return lesser_dummy.next
```
# [88. Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        # Length of nums1 is guaranteed to be # of elements in nums1 and nums2
        last = len(nums1) - 1
        
        # Start from the end of nums1, and fill with the greater value between the last elements of nums1 and nums2;
        # since both lists are sorted, this works
        while m > 0 and n > 0:
            if nums1[m - 1] > nums2[n - 1]:
                nums1[last] = nums1[m - 1]
                m -= 1
            else:
                nums1[last] = nums2[n - 1]
                n -= 1
            last -= 1
        
        # If list1 ran out of elements first, place the rest of list2 elements in
        while n > 0:
            nums1[last] = nums2[n - 1]
            n -= 1
            last -= 1
```
# [96. Unique Binary Search Trees](https://leetcode.com/problems/unique-binary-search-trees/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def numTrees(self, n: int) -> int:
        num_trees = [1] * (n + 1)
        
        # number of trees for 0 and 1 nodes is 1; start at 2
        for nodes in range(2, n + 1):
            total = 0
            for root in range(1, nodes + 1):
                # "nodes" is the highest number, "root" is the currently selected number
                left = root - 1
                right = nodes - root
                # The total number of trees for a given number of nodes is 
                # number of trees on the left side * number of trees on the right side
                total += num_trees[left] * num_trees[right]
            num_trees[nodes] = total
        return num_trees[n]
```
# [98. Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isValidBST(self, root: TreeNode) -> bool:
        def is_valid(node, left, right):
            if not node:
                return True
            if not (left < node.val and right > node.val):
                return False
            return (is_valid(node.left, left, node.val) and is_valid(node.right, node.val, right))
        
        return is_valid(root, float("-inf"), float("inf"))
```
# [100. Same Tree](https://leetcode.com/problems/same-tree/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSameTree(self, p: TreeNode, q: TreeNode) -> bool:
        def validate(p, q):
            if not p and not q:
                return True
            if p and q and p.val == q.val:
                return validate(p.left, q.left) and validate(p.right, q.right)
            return  False
        return validate(p, q)
```
# [102. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        output = []
        # Use queue for storing bfs visits
        queue = collections.deque()
        queue.append(root)
        while queue:
            # The length of the queue is equal to the nodes on the current level; 
            # needed to make sure that the level only contains nodes of that level, 
            # as additional nodes are added for the next level while processing the current one
            queue_length = len(queue)
            current_level = []
            # Process all nodes at the current level, appending their value to the list and 
            # adding their children to the queue
            for i in range(queue_length):
                node = queue.popleft()
                # If nodes have no children, null nodes will be added to the queue; check for this
                if node:
                    current_level.append(node.val)
                    queue.append(node.left)
                    queue.append(node.right)
            # Need to check if current_level isn't empty so an empty list isn't pushed into the output;
            # this would occur if all nodes in the queue are null
            if current_level:
                output.append(current_level)
        return output
```
# [103. Binary Tree Zigzag Level Order Traversal](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    # Solution is the same as "Binary Tree Level Order Traversal", except 
    # the levels are reversed in alternating order using a boolean flag
    def zigzagLevelOrder(self, root: TreeNode) -> List[List[int]]:
        output = []
        queue = collections.deque()
        queue.append(root)
        should_reverse = False
        while queue:
            queue_length = len(queue)
            current_level = []
            for i in range(queue_length):
                node = queue.popleft()
                if node:
                    current_level.append(node.val)
                    queue.append(node.left)
                    queue.append(node.right)
            if current_level:
                if should_reverse:
                    current_level.reverse()
                output.append(current_level)
                should_reverse = not should_reverse
        return output
```
# [104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxDepth(self, root: TreeNode) -> int:
        def check_depth(node):
            if not node:
                return 0
            # Add 1 to account for current node's height, recurse down the left and right children;
            # the max depth at this node is 1 + max depth of left or right child
            return 1 + max(check_depth(node.left), check_depth(node.right))
        return check_depth(root)
```
# [105. Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> TreeNode:
        # The first element of the preorder is the root of the tree; can recursively generate tree off this;
        # the preorder index's first value tells where the tree's root value is,
        # and the root value's inorder position tells you the elements on the left/right side of the root
        preorder_index = 0
        
        # Track the indices of the inorder traversal using the values of the tree;
        # the index of preorder[preorder_index] in the inorder list tells you 
        # which elements are on the left and right side of the tree; 
        # store in a dict to access these indices in constant time, as opposed to a linear search for the values
        inorder_index_map = {}
        for index, value in enumerate(inorder):
            inorder_index_map[value] = index
        
        def create_tree(inorder_start, inorder_end):
            nonlocal preorder_index
            # If called with an empty list, the parent has no child on that side; return none
            if inorder_start > inorder_end:
                return None
            
            # The first element of the preorder traversal is the root
            root = TreeNode(preorder[preorder_index])
            # Increment the preorder index to get the root of the next tree for the next iteration
            preorder_index += 1
            
            # The end index of the left values is 1 less than the root node's position in the inorder traversal
            left_tree_end = inorder_index_map[root.val] - 1
            # The start index of the right values is 1 greater than the root node's position in the inorder traversal
            right_tree_start = inorder_index_map[root.val] + 1
            
            # Generate the left child first, then the right tree to follow preorder traversal order;
            # the left side takes the numbers to the left of the root, and the right side takes the right numbers
            root.left = create_tree(inorder_start, left_tree_end)
            root.right = create_tree(right_tree_start, inorder_end)
            
            return root
        
        return create_tree(0, len(preorder) - 1)
```
# [106. Construct Binary Tree from Inorder and Postorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    # Algorithm is the same as "Construct Binary Tree from Preorder and Inorder Traversal", but
    # with postorder you need to check the end of the list instead of the start (decrement the index instead of increment), 
    # and right child must be generated before left
    def buildTree(self, inorder: List[int], postorder: List[int]) -> TreeNode:
        postorder_index = len(postorder) - 1
        
        inorder_index_map = {}
        for index, value in enumerate(inorder):
            inorder_index_map[value] = index
        
        def create_tree(inorder_start, inorder_end):
            nonlocal postorder_index
            
            if inorder_start > inorder_end:
                return None
            
            root = TreeNode(postorder[postorder_index])
            postorder_index -= 1
            
            
            root.right = create_tree(inorder_index_map[root.val] + 1, inorder_end)
            root.left = create_tree(inorder_start, inorder_index_map[root.val] - 1)
            return root
        
        return create_tree(0, len(postorder) - 1)
```
# [107. Binary Tree Level Order Traversal II](https://leetcode.com/problems/binary-tree-level-order-traversal-ii/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    # The solution is the same as "Binary Tree Level Order Traversal", except the output is reversed at the end
    def levelOrderBottom(self, root: TreeNode) -> List[List[int]]:
        output = []
        queue = collections.deque()
        queue.append(root)
        while queue:
            queue_length = len(queue)
            current_level = []
            for i in range(queue_length):
                node = queue.popleft()
                if node:
                    current_level.append(node.val)
                    queue.append(node.left)
                    queue.append(node.right)
            if current_level:
                output.append(current_level)
        output.reverse()
        return output
```
# [108. Convert Sorted Array to Binary Search Tree](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def sortedArrayToBST(self, nums: List[int]) -> TreeNode:
        def create_node(start, end):
            # If start is higher than end, there's no elements
            if start > end:
                return None
            # Find the middle and make it the root; if even number, floor the index
            mid = (start + end) // 2
            root = TreeNode(nums[mid])
            # Take the elements to the left and right of the middle to create the left and right children
            root.left = create_node(start, mid - 1)
            root.right = create_node(mid + 1, end)
            return root
        return create_node(0, len(nums) - 1)
```
# [111. Minimum Depth of Binary Tree](https://leetcode.com/problems/minimum-depth-of-binary-tree/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def minDepth(self, root: TreeNode) -> int:
        # Need this to account for input being empty list
        if not root:
            return 0
        
        def check_depth(node):
            # If node is null, return max value to signify invalid path
            if not node:
                return float('inf')
            # If the node has no children (leaf node), return 1
            if not node.left and not node.right:
                return 1
            # The minimum depth of the current node is 1 (itself) + minimum depth of children
            return 1 + min(check_depth(node.left), check_depth(node.right))
        return check_depth(root)
```
# [112. Path Sum](https://leetcode.com/problems/path-sum/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def hasPathSum(self, root: TreeNode, targetSum: int) -> bool:
        def check_sum(node, current_target):
            # Return null if parent has no child
            if not node:
                return False
            
            # If target - value = 0 and the current node is a leaf, return true
            change = current_target - node.val
            if change == 0 and not node.left and not node.right:
                return True
            
            # Recurse down children with the new target being the difference of the target and node's value
            return check_sum(node.left, change) or check_sum(node.right, change)
        return check_sum(root, targetSum)
```
# [113. Path Sum II](https://leetcode.com/problems/path-sum-ii/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def pathSum(self, root: TreeNode, targetSum: int) -> List[List[int]]:
        result = []
        def check_sum(node, current_target, current_path):
            # Return null if parent has no child
            if not node:
                return
            # Add the current value to the path, so the path can be returned if a valid path is found
            current_path.append(node.val)
            # If target - value = 0 and the current node is a leaf, append the current path to the result
            change = current_target - node.val
            if change == 0 and not node.left and not node.right:
                result.append(current_path.copy())
            else:
                # Recurse down children with the new target being the difference of the target and node's value
                check_sum(node.left, change, current_path) 
                check_sum(node.right, change, current_path)
            # Pop the node's value after traversing its children to prevent the value from polluting other paths
            current_path.pop()
        check_sum(root, targetSum, [])
        return result
```
# [116. Populating Next Right Pointers in Each Node](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
```
# [117. Populating Next Right Pointers in Each Node II(https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
```
# [120. Triangle](https://leetcode.com/problems/triangle/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def minimumTotal(self, triangle: List[List[int]]) -> int:
        # Initialize DP array of size len(triangle) + 1; 
        # extra space to account for base case of 0s row
        dp = [0] * (len(triangle) + 1)
        
        # Iterate through triangle rows backwards
        for row in triangle[::-1]:
            # To calculate the cost of the minimum path at an index, 
            # add the current number at row[i] to the minimum of dp[i] and dp[i+1]
            for i, num in enumerate(row):
                dp[i] = num + min(dp[i], dp[i + 1])
        # The minimum cost of the first row is stored in the first index
        return dp[0]
```
# [121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        known_max_profit = 0
        # Use 2 indices to track current_minimum and current_maximum;
        # current is used because indices will be "reset" to the index of 
        # the known lowest value whenever it's discovered
        current_minimum, current_maximum = 0, 0
        
        for i, price in enumerate(prices):
            if price < prices[current_minimum]:
                current_minimum, current_maximum = i, i
            if price > prices[current_maximum]:
                current_maximum = i
                known_max_profit = max(known_max_profit, (prices[current_maximum] - prices[current_minimum]))
                
        return known_max_profit
```
# [124. Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxPathSum(self, root: TreeNode) -> int:
        # Negative numbers are possible, so start from lowest possible value rather than 0
        max_sum = float('-inf')
        def max_gain(node):
            nonlocal max_sum
            # If the parent has no children, can't select what doesn't exist (return 0 to force no selection)
            if not node:
                return 0
            # The max gain of child nodes is either their max gain (if chosen to include) or 0 (if chosen to not include)
            left_max_gain = max(max_gain(node.left), 0)
            right_max_gain = max(max_gain(node.right), 0)
            # Check to see if node + max sum of both children is the known max; if it is, assign it
            # if a new max is found later, it'll be overwritten
            new_path_max_sum = left_max_gain + node.val + right_max_gain
            max_sum = max(max_sum, new_path_max_sum)
            # The max gain that a node can give (while continuing the path) is 
            # the node's value + the max of the left side or right side; 
            # both sides can only be selected if you start a new path
            return node.val + max(left_max_gain, right_max_gain)
        max_gain(root)
        return max_sum
```
# [125. Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def isPalindrome(self, s: str) -> bool:
        # Initialize 2 indices at the start and end of the string for comparison
        left, right = 0, len(s) - 1
        
        while left < right:
            # Filtering for alphanumeric characters only
            while left < right and not s[left].isalnum():
                left += 1
            while left < right and not s[right].isalnum():
                right -= 1
            if s[left].lower() != s[right].lower():
                return False
            left += 1
            right -= 1
        return True
```
# [128. Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        # Create a set from the list of numbers to easily iterate over unique numbers
        existing_nums = set(nums)
        longest_sequence = 0
        # For each number, check if the number before it (number - 1) exists; 
        # if it does, it's part of a longer sequence (ignore these); if it doesn't, it's the start of a sequence;
        # repeatedly search for the numbers after it; if they exist, increment counter by 1 until sequence breaks;
        # when sequence breaks, take the max of known longest sequence and current sequence
        for num in existing_nums:
            if (num - 1) not in existing_nums:
                sequence = 0
                while (num + sequence) in existing_nums:
                    sequence += 1
                longest_sequence = max(longest_sequence, sequence)
        return longest_sequence
```
# [129. Sum Root to Leaf Numbers](https://leetcode.com/problems/sum-root-to-leaf-numbers/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def sumNumbers(self, root: TreeNode) -> int:
        def dfs(node, num):
            # If the node is null, return 0
            if not node:
                return 0
            # Multiply the given number by 10 to open the least significant digit, then add node's value to it
            num = num * 10 + node.val
            # If leaf node, return the number to prevent returning 0s
            if not node.left and not node.right:
                return num
            # If not leaf node, recurse down the left and right sides to get the full number; 
            # the completed numbers will get added up here in pairs of 2 and be sent up to the root
            return dfs(node.left, num) + dfs(node.right, num)
        return dfs(root, 0)
```
# [131. Palindrome Partitioning](https://leetcode.com/problems/palindrome-partitioning/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def partition(self, s: str) -> List[List[str]]:
        # Store all valid partitions in result, and track the current partition combination in current_partition
        result = []
        current_partition = []
        
        def generate_partitions(i):
            # If the current index goes out of bounds of the given string, no combinations left;
            # store it in result and start going back
            if i >= len(s):
                result.append(current_partition.copy())
                return
            # Check every combination in the range of i to the end of the string for palindromes;
            # if a valid range is found, append that substring to the current partition, and 
            # repeat for the range after that substring
            for j in range(i, len(s)):
                if self.is_palindrome(s, i, j):
                    current_partition.append(s[i:j+1])
                    generate_partitions(j + 1)
                    current_partition.pop()
        generate_partitions(0)
        return result
        
    def is_palindrome(self, s, start, end):
        while start < end:
            if s[start] != s[end]:
                return False
            start += 1
            end -= 1
        return True
```
# [133. Clone Graph](https://leetcode.com/problems/clone-graph/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
"""
# Definition for a Node.
class Node:
    def __init__(self, val = 0, neighbors = None):
        self.val = val
        self.neighbors = neighbors if neighbors is not None else []
"""
class Solution:
    def cloneGraph(self, node: 'Node') -> 'Node':
        # Track the clones in a dictionary to prevent duplicate clones
        copies = {}
        def clone_dfs(node):
            # If the node has already been cloned, return the clone
            if node in copies:
                return copies[node]
            copy = Node(node.val)
            copies[node] = copy
            # Recursively clone all neighbors and append them to the clone
            for neighbor in node.neighbors:
                copy.neighbors.append(clone_dfs(neighbor))
            return copy
        # clone_dfs() needs to return a clone to function, so can just call it on root node;
        # also edge case for empty list
        return clone_dfs(node) if node else None
```
# [138. Copy List with Random Pointer](https://leetcode.com/problems/copy-list-with-random-pointer/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
"""
# Definition for a Node.
class Node:
    def __init__(self, x: int, next: 'Node' = None, random: 'Node' = None):
        self.val = int(x)
        self.next = next
        self.random = random
"""

class Solution:
    def copyRandomList(self, head: 'Node') -> 'Node':
        # Store references to copy nodes with a dict with keys being the original nodes;
        # mapping null to null for edge case of null keys in next/random; 
        # should be able to alternatively do an if null check before assignment
        copy_nodes = { None: None }
        # Loop through once to create all copy nodes, without mapping
        cur = head
        while cur:
            copy_nodes[cur] = Node(cur.val)
            cur = cur.next
        # Loop again to map copy nodes next/random pointers to their respective copies
        cur = head
        while cur:
            copy_node = copy_nodes[cur]
            copy_node.next = copy_nodes[cur.next]
            copy_node.random = copy_nodes[cur.random]
            cur = cur.next
        # Return the copy of the head from the dict
        return copy_nodes[head]
```
# [141. Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def hasCycle(self, head: ListNode) -> bool:
        # Use 2 nodes; fast_node will increment by 2 every iteration, slow_node by 1
        slow_node = head
        fast_node = head
        
        while fast_node:
            slow_node = slow_node.next
            fast_node = fast_node.next
            
            # If fast_node isn't null (not end of list), increment again; 
            # if fast_node == slow_node (fast_node caught up to slow_node), there's a cycle; return true. 
            # If there's no cycle, fast_node will become null and won't cross paths with slow_node
            if fast_node:
                fast_node = fast_node.next
                if fast_node == slow_node:
                    return True
        return False
```
# [142. Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def detectCycle(self, head: ListNode) -> ListNode:
        slow, fast = head, head
        # Check if a cycle is present; if there is one, break out
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            if fast == slow:
                break
        # If the loop ended because of null and not a cycle, return null
        if not fast or not fast.next:
            return None
        
        # Reset slow node to the start, and increment both pointers by 1 until they meet
        slow = head
        while slow != fast:
            slow = slow.next
            fast = fast.next
        return fast
```
# [143. Reorder List](https://leetcode.com/problems/reorder-list/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reorderList(self, head: ListNode) -> None:
        """
        Do not return anything, modify head in-place instead.
        """
        # Find middle of linked list algorithm
        slow_node, fast_node = head, head
        while fast_node and fast_node.next:
            slow_node = slow_node.next
            fast_node = fast_node.next.next
        
        # Reverse linked list algorithm
        prev_node = None
        current_node = slow_node
        while current_node:
            next_node = current_node.next
            current_node.next = prev_node
            prev_node = current_node
            current_node = next_node
        
        first_node = head
        second_node = prev_node
        
        while second_node.next:
            # Set the first node's next node to the second node, and increment the first node (before changing its next node)
            first_node.next, first_node = second_node, first_node.next
            # Set the second node's next node to the (incremented) first node, and increment the second node (before changing its next node)
            second_node.next, second_node = first_node, second_node.next
```
# [146. LRU Cache](https://leetcode.com/problems/lru-cache/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Utilize doubly-linked list to track recency
class Node:
    def __init__(self, key, val):
        self.key, self.val = key, val
        self.prev = None
        self.next = None
        
class LRUCache:
    # Use dict to store cache values; initialize 2 placeholder nodes for left/right
    def __init__(self, capacity: int):
        self.capacity = capacity
        self.cache = {}
        
        self.left, self.right = Node(0, 0), Node(0, 0)
        self.left.next = self.right
        self.right.prev = self.left
    
    # Remove the given node from the linked list
    def remove(self, node):
        next_node = node.next
        prev_node = node.prev
        
        prev_node.next = next_node
        next_node.prev = prev_node
    
    # Insert the given node into the linked list on the right side
    # TODO: why in the middle of the rightmost instead of to the right of the rightmost?
    def insert(self, node):
        prev_node = self.right.prev
        next_node = self.right
        
        prev_node.next = node
        next_node.prev = node
        
        node.next = next_node
        node.prev = prev_node
        return

    def get(self, key: int) -> int:
        # Whenever a key is accessed, remove and re-insert the node that was accessed;
        # Removing a node from the linked list doesn't remove it from the dict, so no issue
        if key in self.cache:
            self.remove(self.cache[key])
            self.insert(self.cache[key])
            return self.cache[key].val
        return -1
        

    def put(self, key: int, value: int) -> None:
        # If the key is already in the cache, remove it from the linked list to prevent duplicates
        if key in self.cache:
            self.remove(self.cache[key])
        # Create a new node to store in the dict, and connect it to the linked list
        self.cache[key] = Node(key, value)
        self.insert(self.cache[key])
        
        # If the cache is over capacity, remove the leftmost node from the linked list 
        # and its value removed from the cache
        if len(self.cache) > self.capacity:
            lru = self.left.next
            self.remove(lru)
            del self.cache[lru.key]


# Your LRUCache object will be instantiated and called as such:
# obj = LRUCache(capacity)
# param_1 = obj.get(key)
# obj.put(key,value)
```
# [148. Sort List](https://leetcode.com/problems/sort-list/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def sortList(self, head: ListNode) -> ListNode:
        if not head or not head.next:
            return head
        left = head
        right = self.find_mid(head)
        temp = right.next
        right.next = None
        right = temp
        
        left = self.sortList(left)
        right = self.sortList(right)
        return self.merge_lists(left, right)
    # See Middle of the Linked List for details
    # TODO: why does fast start at head.next and not head?
    def find_mid(self, head):
        fast, slow = head.next, head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
        return slow
    # See Merge Two Sorted Lists for details
    def merge_lists(self, list1, list2):
        dummy = ListNode()
        tail = dummy
        while list1 and list2:
            if list1.val > list2.val:
                tail.next = list2
                list2 = list2.next
            else:
                tail.next = list1
                list1 = list1.next
            tail = tail.next
        if list1:
            tail.next = list1
        if list2:
            tail.next = list2
        return dummy.next
```
# [152. Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        max_product = max(nums)
        # Store both the minimum and maximum of the current; because of negatives, 
        # the possible maximum could come from either the minimum or maximum
        # 1s are neutral in multiplication, so use this
        prev_min_product, prev_max_product = 1, 1
        for num in nums:
            # Store previous max in temp variable to use it when calculating new previous min
            temp = prev_max_product
            # Choices: multiply current number with the previous product, or ignore it (if it's a 0)
            prev_max_product = max(prev_min_product * num, prev_max_product * num, num)
            prev_min_product = min(prev_min_product * num, temp * num, num)
            max_product = max(max_product, prev_max_product)
        return max_product
```
# [153. Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    # Searching for the inflection point; where a given value's previous element is > itself
    def findMin(self, nums: List[int]) -> int:
        # If there's only 1 element, return it
        if len(nums) == 1:
            return nums[0]
        
        left, right = 0, len(nums) - 1
        
        # If the last element is greater than the first element, there's no rotation
        if nums[left] < nums[right]:
            return nums[left]
        
        while left <= right:
            mid = left + (right - left) // 2
            
            # If this element is greater than the next element, return next element
            if nums[mid] > nums[mid + 1]:
                return nums[mid + 1]
            
            # If this element is lesser than its previous element, return this element
            if nums[mid - 1] > nums[mid]:
                return nums[mid]
            
            # If the middle value is greater than the left side, no rotation here; search right side
            if nums[left] < nums[mid]:
                left = mid + 1
            else:
                right = mid - 1
        return -1
```
# [154. Find Minimum in Rotated Sorted Array II](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def findMin(self, nums: List[int]) -> int:
        # If there's only 1 element, return it
        if len(nums) == 1:
            return nums[0]
        
        left, right = 0, len(nums) - 1
        
        # If the last element is greater than the first element, there's no rotation
        if nums[left] < nums[right]:
            return nums[left]
        
        # TODO: ? something about invariants; can't really know without more reading. come back here later
        while left < right:
            mid = left + (right - left) // 2
            
            if nums[mid] < nums[right]:
                right = mid
            elif nums[mid] > nums[right]:
                left = mid + 1
            else:
                right -= 1
        return nums[left]
```
# [167. Two Sum II - Input array is sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        left, right = 0, len(numbers) - 1
        while left < right:
            ans = numbers[left] + numbers[right]
            if ans == target:
                return [left + 1, right + 1]
            if ans > target:
                right -= 1
            else:
                left += 1
```
# [169. Majority Element](https://leetcode.com/problems/majority-element/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# https://en.wikipedia.org/wiki/Boyer%E2%80%93Moore_majority_vote_algorithm
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        # Track the number that has currently been seen the most, and the number of occurences
        current_majority_num = None
        current_majority_count = 0
        
        for num in nums:
            # If the count of the current majority is 0, set the current number to be the majority number
            if current_majority_count == 0:
                current_majority_num = num
            # If the current number is the same as the current majority number, increment its count; 
            # otherwise, decrement its count
            if num == current_majority_num:
                current_majority_count += 1
            else:
                current_majority_count -= 1
        # The number in the current majority is the number with the most occurences;
        # guaranteed to be correct because there will only ever be 1 majority element in this problem's case
        return current_majority_num
```
# [198. House Robber](https://leetcode.com/problems/house-robber/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def rob(self, nums: List[int]) -> int:
        previous_selection, two_back_rob = 0, 0
        max_rob = 0
        for current_num in nums:
            # The maximum amount to rob at the current house is either to reset and start again as 
            # current house + 2 houses back, or select none and keep the value of previous house + all previous robs 
            # (any other combination would lead to a conflict)
            max_rob = max(previous_selection, two_back_rob + current_num)
            # The new "2 houses back" for the next loop will be the current previous house 
            # (which includes all previous robs)
            two_back_rob = previous_selection
            # The new previous selection for the next loop will be the currently selected option
            previous_selection = max_rob
        return max_rob
```
# [199. Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def rightSideView(self, root: TreeNode) -> List[int]:
        # Solutiotn is the same as Binary Tree Level Order Traversal, but you only care about the last value
        result = []
        queue = collections.deque()
        queue.append(root)
        while queue:
            rightmost_node = None
            queue_length = len(queue)
            for i in range(queue_length):
                node = queue.popleft()
                if node:
                    queue.append(node.left)
                    queue.append(node.right)
                    rightmost_node = node
            if rightmost_node:
                result.append(rightmost_node.val)
        return result
```
# [200. Number of Islands](https://leetcode.com/problems/number-of-islands/)
## Information
## Question
## Solutions
scan array; if 1, bfs/dfs visit all other 1s in the area; # of islands = # of bfs/dfs searches. whether you bfs or dfs shouldn't matter, since you need to check every grid tile
union find? dunno what this is yet though
## Notes
## Solution Code
``` py
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        rows, cols = len(grid), len(grid[0])
        # For tracking tiles that have been visited in bfs()
        visited_tiles = set()
        num_islands = 0
        
        def unvisited_land(row, col):
            return True if grid[row][col] == "1" and (row, col) not in visited_tiles else False
        
        def bfs(row_to_visit, col_to_visit):
            tiles_to_visit = collections.deque()
            tile = (row_to_visit, col_to_visit)
            tiles_to_visit.append(tile)
            visited_tiles.add(tile)
            while tiles_to_visit:
                # In BFS, retrieve the oldest tile and add its surrounding tiles to the queue;
                # to DFS, you would retrieve the newest tile instead (tiles_to_visit.pop() to get right side)
                row, col = tiles_to_visit.popleft()
                directions_to_travel = [[0, -1], [0, 1], [1, 0], [-1, 0]]
                for dr, dc in directions_to_travel:
                    next_row, next_col = row + dr, col + dc
                    if next_row in range(rows) and next_col in range(cols) and unvisited_land(next_row, next_col):
                        next_tile = (next_row, next_col)
                        tiles_to_visit.append(next_tile)
                        visited_tiles.add(next_tile)
                
        for row in range(rows):
            for col in range(cols):
                if unvisited_land(row, col):
                    bfs(row, col)
                    num_islands += 1
        return num_islands
```
# [202. Happy Number](https://leetcode.com/problems/happy-number/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def isHappy(self, n: int) -> bool:
        # Use a set to record numbers that have appeared previously; 
        # if the same number appears twice, it will be an infinite loop
        visited = set()
        while n not in visited:
            visited.add(n)
            # Calculate the new value of n and repeat the loop if needed
            n = self.sum_squares(n)
            
            # If n = 1, it'll stay there; return true
            if n == 1:
                return True
    
    # Mod n by 10 to get the least significant digit, then use integer division to decrease n by a factor of 10 until 0
    def sum_squares(self, n):
        result = 0
        while n:
            result += ((n % 10) ** 2)
            n = n // 10
        return result
```
# [203. Remove Linked List Elements](https://leetcode.com/problems/remove-linked-list-elements/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeElements(self, head: ListNode, val: int) -> ListNode:
        dummy = ListNode(0, head)
        previous_node, current_node = dummy, head
        
        while current_node:
            # If the current node's value should be removed, redirect the previous node's pointer to the next node;
            # if not, set the previous node to the current node
            if current_node.val == val:
                previous_node.next = current_node.next
            else:
                previous_node = current_node
            # Set current node to the next node
            current_node = current_node.next
        return dummy.next
```
# [206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        # Need to track the previous node in order to be able to redirect pointers backwards
        previous_node = None
        current_node = head
        
        while current_node:
            # Store the next node in a temporary variable (to maintain access to it after pointer to it is redirected)
            next_node = current_node.next
            # Set the current node's next node to the previous node (reversing the direction here)
            current_node.next = previous_node
            # Set the previous node to the current node, and set the current node to the next node (iterate both by 1)
            previous_node = current_node
            current_node = next_node
        return previous_node
```
# [207. Course Schedule](https://leetcode.com/problems/course-schedule/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        # Populate a dictionary of key = course, value = list of prerequisite courses
        courses = defaultdict(list)
        for course, prereq in prerequisites:
            courses[course].append(prereq)
        
        # Track previously visited locations for dfs break condition; 
        # if the same course appears twice, there's a cycle
        visited = set()
        def can_complete_dfs(course):
            # Base cases: If the course has no prerequisites, return true; 
            # if the course has been visited before, there's a cycle; return false;
            if not courses[course]:
                return True
            if course in visited:
                return False
            # Visit the location, then check to see if all of its prerequisites can be completed;
            # the only case for not completing is if there's a cycle, so if there is one, return false
            visited.add(course)
            for prereq in courses[course]:
                if not can_complete_dfs(prereq):
                    return False
            # If all prerequisites can be completed, the course can be completed; 
            # empty the prerequisite list to indicate that
            courses[course] = []
            return True
        # Iterate through all courses and check if they can be completed;
        # looping like this is fine because there's guaranteed to be courses 0 to numCourses
        for course in range(numCourses):
            if not can_complete_dfs(course):
                return False
        return True
```
# [208. Implement Trie (Prefix Tree)](https://leetcode.com/problems/implement-trie-prefix-tree/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
```
# [209. Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
```
# [210. Course Schedule II](https://leetcode.com/problems/course-schedule-ii/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def findOrder(self, numCourses: int, prerequisites: List[List[int]]) -> List[int]:
        # Store course prerequisites in a dictionary of key = course number, value = list of prerequisites
        course_prerequisites = { course: [] for course in range(numCourses) }        
        for course, prereq in prerequisites:
            course_prerequisites[course].append(prereq)
        # Track courses that are currently being visited (to detect cycles) and courses that have been visited
        currently_visiting, visited = set(), set()
        result = []
        def search_courses(course):
            # If the course is still being visited from earlier and you came back to it, there's a cycle; return false
            if course in currently_visiting:
                return False
            # If the course has already been fully visited earlier, it can be completed; return true
            if course in visited:
                return True
            # Add the current course to the courses being visited, and visit all of its prerequisites 
            # to check if they can be completed
            currently_visiting.add(course)
            for prereq in course_prerequisites[course]:
                if not search_courses(prereq):
                    return False
            # After confirming all prerequisites can be completed, remove it from currently_visiting, add it to visited, and
            # append it to the order of courses
            currently_visiting.remove(course)
            visited.add(course)
            result.append(course)
            return True
        # Iterate through all courses and check if they can be completed; if any course cannot be completed, return empty
        for course in range(numCourses):
            if not search_courses(course):
                return []
        return result
```
# [211. Design Add and Search Words Data Structure](https://leetcode.com/problems/design-add-and-search-words-data-structure/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
```
# [213. House Robber II](https://leetcode.com/problems/house-robber-ii/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# The question is the same as House Robber 1, but the max of (all but first house) and (all but last house)
# needs to be taken, and a new edge case of only 1 house due to the new restriction
class Solution:
    def rob(self, nums: List[int]) -> int:
        def max_rob(nums):
            one_back_rob, two_back_rob = 0, 0
            max_rob = 0
            for current_num in nums:
                max_rob = max(one_back_rob, two_back_rob + current_num)
                two_back_rob = one_back_rob
                one_back_rob = max_rob  
            return max_rob
        # If there's only one house, it will be missed by the max function call
        # (excluding first and excluding last will be 0 in array size 1)
        if len(nums) == 1:
            return nums[0]
        return max(max_rob(nums[1:]), max_rob(nums[:-1]))
```
# [217. Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        # Use dictionary to track previous elements
        num_count = {}
        for num in nums:
            # If the current number already exists in the dictionary, it's a duplicate; return true
            # else, add the number to the dictionary
            if num in num_count:
                return True
            num_count[num] = 1
        return False
```
# [221. Maximal Square](https://leetcode.com/problems/maximal-square/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def maximalSquare(self, matrix: List[List[str]]) -> int:
        rows, cols = len(matrix), len(matrix[0])
        cache = {}
        def search_squares(row, col):
            # If the current search is out of bounds, return 0
            if row >= rows or col >= cols:
                return 0
            # Get the max area for the tiles to the right, down, and diagonally (right+down)
            if (row, col) not in cache:
                right = search_squares(row, col + 1)
                down = search_squares(row + 1, col)
                diagonal = search_squares(row + 1, col + 1)
                
                cache[(row, col)] = 0
                # If the current tile contains a 1, the max square area for the tile is 
                # 1 + minimum of right, down, and diagonal tiles
                if matrix[row][col] == "1":
                    cache[(row, col)] = 1 + min(right, down, diagonal)
                
            return cache[(row, col)]
        search_squares(0, 0)
        return max(cache.values()) ** 2
```
# [226. Invert Binary Tree]
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def invertTree(self, root: TreeNode) -> TreeNode:
        # Base case; if the node is null, return; this means that 
        # the node that called the function has no child at the location.
        # Not having this leads to null references
        if not root:
            return None
        
        # Swapping nodes
        temp = root.left
        root.left = root.right
        root.right = temp
        
        # Loop cases; inverting the child nodes of current node's children
        self.invertTree(root.left)
        self.invertTree(root.right)
        
        return root
```
# [230. Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def kthSmallest(self, root: TreeNode, k: int) -> int:
        counter = 0
        stack = []
        node = root
        # Since k is always guaranteed to be <= n, loop should run indefinitely
        while node or stack:
            # Repeatedly add the current node to the stack, then traverse down the left side
            while node:
                stack.append(node)
                node = node.left
            # When there are no more nodes on the left side, process middle node; 
            # increment a counter to indicate the current iteration; if counter == k, 
            # you're on the kth node, so return it 
            node = stack.pop()
            counter += 1
            if counter == k:
                return node.val
            # Traverse down the right side after processing the left and middle
            node = node.right
```
# [234. Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def isPalindrome(self, head: ListNode) -> bool:
        # find middle > reverse the latter half > iterate through both and compare values
        
        # Process for finding middle of linked list (see Middle of the Linked List)
        fast, slow = head, head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
        
        # Process for reversing linked list (see Reverse Linked List)
        prev_node = None
        while slow:
            next_node = slow.next
            slow.next = prev_node
            prev_node = slow
            slow = next_node
        
        # Process for checking for palindromes; 
        left_node, right_node = head, prev_node
        # Check right_node since it's shorter than left_node
        while right_node:
            if left_node.val != right_node.val:
                return False
            left_node = left_node.next
            right_node = right_node.next
        return True
```
# [235. Lowest Common Ancestor of a Binary Search Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        def lca(root, p, q):
            # Parent node has no child on the given side; return null
            if not root:
                return
            # If both p and q are greater than the root, traverse down the right side
            if p.val > root.val and q.val > root.val:
                return lca(root.right, p, q)
            # If both p and q are lesser than the root, traverse down the left side
            elif p.val < root.val and q.val < root.val:
                return lca(root.left, p, q)
            # If p and q split up (both arent greater or lesser than the root), 
            # the root is the LCA, as they go in different directions from that point
            else:
                return root
        return lca(root, p, q)
```
# [236. Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
```
# [238. Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        length = len(nums)
        
        # Store the products of all elements to the left of a given index, and 
        # the values of all elements to the right of a given index
        left_products, right_products, result = [0] * length, [0] * length, [0] * length
        
        # The product of all elements to the left of the first index and 
        # all elements to the right of the last index is 1 as a default
        left_products[0] = 1
        right_products[length - 1] = 1
        
        # Start from the second element, since first element is already known
        for i in range(1, length):
            # The product of all elements to the left of an index is 
            # the number at the previous index (new) * all products of previous indices
            left_products[i] = nums[i - 1] * left_products[i - 1]
        
        # Fill right products backwards, from the second last element, since the last element is already known
        for i in range(length - 2, -1, -1):
            right_products[i] = nums[i + 1] * right_products[i + 1]
            
        print(left_products, right_products)
        
        # Generate result array; the result of a given index i is left products[i] * right products[i];
        # due to how the left/right products were generated, a given index will never include itself,
        # since a given index is calculated using all elements before/after it for left/right side respectively
        for i in range(length):
            result[i] = left_products[i] * right_products[i]
        return result
```
# [239. Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        output = []
        # Save the indices of the maximum values in the current window using a deque
        max_queue = collections.deque()
        left, right = 0, 0
        
        while right < len(nums):
            # Continuously compare the last element of the dequeue with the new value about to be added; 
            # if the new value is greater, remove the last element
            while max_queue and nums[max_queue[-1]] < nums[right]:
                max_queue.pop()
            # Add the new value to the top of the deque
            max_queue.append(right)
            
            # If the index of the dequeue's bottom is no longer within the window, remove it
            if left > max_queue[0]:
                max_queue.popleft()
            
            # If the window is fully expanded, add the oldest maximum value to the output; 
            # due to the way new elements are added to the maximum value deque, the highest value will 
            # always be at the first position
            if (right + 1) >= k:
                output.append(nums[max_queue[0]])
                # Move the window along by 1 (left side doesn't move if window isn't fully expanded)
                left += 1
            right += 1
        return output
```
# [242. Valid Anagram](https://leetcode.com/problems/valid-anagram/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# This is the solution that can be expanded to support any character; for the version that's O(1) space 
# and only considers lowercase alphabetical characters, see solution for LC 49 (Group Anagrams), as it's basically the same thing
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        s_length, t_length = len(s), len(t)
        # If both strings are not the same length, they can't be anagrams
        if s_length != t_length:
            return False
        # Use dictionary to store character counts
        char_count = defaultdict(int)
        
        # Have character appearances in the first string increment the count, 
        # and appearances in the second string decrement by the same amount
        for i in range(s_length):
            char_count[s[i]] += 1
            char_count[t[i]] -= 1
        # Iterate the entire dictionary; if a value isn't 0, they're not anagrams
        # (if they were, the increment/decrements would cancel out to 0)
        for key in char_count:
            if char_count[key] != 0:
                return False
        return True
```
# [252. Meeting Rooms](https://leetcode.com/problems/meeting-rooms/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def canAttendMeetings(self, intervals: List[List[int]]) -> bool:
        # Sort list of intervals by start, so overlaps can easily be found
        intervals.sort(key = lambda i : i[0])
        for i in range(len(intervals) - 1):
            # If the current interval's end is greater than the next interval's start,
            # there's an overlap, so can't attend the next meeting; return false
            if intervals[i][1] > intervals[i + 1][0]:
                return False
        return True
```
# [268. Missing Number](https://leetcode.com/problems/missing-number/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def missingNumber(self, nums: List[int]) -> int:
        # Create a set from the list of numbers
        num_set = set(nums)
        # Check all numbers from 0 to n; if the number isn't in the set, it's the missing number
        for i in range(len(nums) + 1):
            if i not in num_set:
                return i
```
# [287. Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def findDuplicate(self, nums: List[int]) -> int:
        slow, fast = nums[0], nums[0]
        
        # Since the values of the numbers are guaranteed to be a valid index, can look for a cycle by
        # setting 2 indices to the index of their values
        while True:
            slow =  nums[slow]
            fast = nums[nums[fast]]
            if slow == fast:
                break
        
        # Reset the slow pointer to the beginning, and increment both slow and fast (now moving slow) pointers
        # until they meet, then return the index's value (see "Linked List Cycle II")
        slow = nums[0]
        while slow != fast:
            slow = nums[slow]
            fast = nums[fast]
        return fast
```
# [300. Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# TODO: implement dp binsearch solution?
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        # Initialize DP array as 1, the shortest possible value of a subsequence
        dp = [1] * len(nums)
        # Start from last element and work up to first element, as earlier elements depend on the result of later elements
        for i in range(len(nums) - 1, -1, -1):
            # Iterate through all elements that come after nums[i] to try combinations with their longest subsequences;
            for j in range(i + 1, len(nums)):
                # If an element that comes after nums[i] is greater than nums[i], it's not increasing; ignore
                if nums[i] < nums[j]:
                    # The current known longest possible subsequence at a given position is either
                    # itself (if a previous selection yielded a higher result) or 1 + longest subsequence of current selection
                    # (this is why it's done backwards?); the actual longest can't be known until all combinations are tried?
                    dp[i] = max(dp[i], 1 + dp[j])
        return max(dp)
```
# [310. Minimum Height Trees](https://leetcode.com/problems/minimum-height-trees/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
```
# [322. Coin Change](https://leetcode.com/problems/coin-change/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        # Initialize DP array of length amount + 1 (calling dp[amount] at end);
        # infinity used as default as dp array stores minimum # of coins for a given amount
        dp = [float("inf")] * (amount + 1)
        # Minimum # of coins to make 0 is 0; base
        dp[0] = 0
        # dp[0] is known, so start at 1; iterate through every coin quantity until amount is reached
        for amt in range(1, amount + 1):
            # Iterate through all possible coins; if valid (>= 0), select either the current known minimum for amount or
            # 1 (accounting for itself) + the currently calculated minimum if it's better
            for coin in coins:
                if amt - coin >= 0:
                    dp[amt] = min(dp[amt], 1 + dp[amt - coin])
        # If no combination was possible for amount, dp[amount] would never be set; return -1 in this case
        return dp[amount] if dp[amount] != float("inf") else -1
```
# [323. Number of Connected Components in an Undirected Graph](https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    # Solution is similar to number of islands, except as a graph traversal rather than 4-directional grid traversal
    def countComponents(self, n: int, edges: List[List[int]]) -> int:
        num_components = 0
        
        # Create adjacency list
        nodes = {}
        for node in range(n):
            nodes[node] = []
        
        for edge in edges:
            nodes[edge[0]].append(edge[1])
            nodes[edge[1]].append(edge[0])
        
        # Track previously visited nodes with a set
        visited = set()
        def dfs(node):
            # If node has been seen before, ignore it
            if node in visited:
                return
            # Visit the node, and dfs through all of its neighbors
            visited.add(node)
            for neighbor in nodes[node]:
                dfs(neighbor)
            
        # Iterate through all nodes; if the node hasn't been visited yet, 
        # increment num_compoenents and dfs the node to visit all of its components
        for node in nodes:
            if node not in visited:
                num_components += 1
                dfs(node)
        # number of components will be equal to the number of dfs searched started
        return num_components
```
# [336. Palindrome Pairs](https://leetcode.com/problems/palindrome-pairs/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
```
# [337. House Robber III](https://leetcode.com/problems/house-robber-iii/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def rob(self, root: TreeNode) -> int:
        # 2 choices: don't include root and take the max of root's children, or
        # include root node and take the max of root's children's children (their max without root)
        def max_rob(node):
            # If node is null, only options are 0
            if not node:
                return [0, 0]
            left_max = max_rob(node.left)
            right_max = max_rob(node.right)
            
            with_root = node.val + left_max[1] + right_max[1]
            without_root = max(left_max) + max(right_max)
            
            return [with_root, without_root]
        return max(max_rob(root))
```
# [392. Is Subsequence](https://leetcode.com/problems/is-subsequence/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        # Search both strings with 2 pointers
        i, j = 0, 0
        while i < len(s) and j < len(t):
            # If the substring and longer string match at the character, increment substring pointer
            if s[i] == t[j]:
                i += 1
            # Always increment the longer string that's being searched
            j += 1
        # If i reached the end of the substring, there was a full match; else, there wasn't
        return True if i == len(s) else False
```
# [421. Maximum XOR of Two Numbers in an Array](https://leetcode.com/problems/maximum-xor-of-two-numbers-in-an-array/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
```
# [424. Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
```
# [425. Word Squares](https://leetcode.com/problems/word-squares/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
```
# [437. Path Sum III](https://leetcode.com/problems/path-sum-iii/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
```
# [442. Find All Duplicates in an Array](https://leetcode.com/problems/find-all-duplicates-in-an-array/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    # Using "indices as value storage" thing since the problem constraints allow for it
    # (all values are between 1 and n inclusive, where n is the array size; 
    # specifically looking for double appearances in an array of single appearances)
    def findDuplicates(self, nums: List[int]) -> List[int]:
        result = []
        for num in nums:
            # If the value in index is negative, it's been seen before; append it to result
            if nums[abs(num) - 1] < 0:
                result.append(abs(num))
            # Multiply the index of num - 1 by -1 to indicate it's been seen before
            nums[abs(num) - 1] *= -1
        return result
```
# [444. Sequence Reconstruction](https://leetcode.com/problems/sequence-reconstruction/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
```
# [448. Find All Numbers Disappeared in an Array](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def findDisappearedNumbers(self, nums: List[int]) -> List[int]:
        result = []
        for num in nums:
            # If the value at the index of num - 1 is positive, negate it to mark as seen 
            # (if it's already negative, already been seen)
            if nums[abs(num) - 1] > 0:
                nums[abs(num) - 1] *= -1
                
        # Loop through all indices; if index of i is positive, its value wasn't in the array; append to result
        for i in range(1, len(nums) + 1):
            if nums[i - 1] > 0:
                result.append(i)
        return result
```
# [463. Island Perimeter](https://leetcode.com/problems/island-perimeter/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def islandPerimeter(self, grid: List[List[int]]) -> int:
        rows = len(grid)
        cols = len(grid[0])
        
        visited = set()
        def perimeter_dfs(row, col):
            # If a tile is a location that's water or out of bounds, adds a perimeter part to surrounding land
            if row >= rows or col >= cols or row < 0 or col < 0 or grid[row][col] == 0:
                return 1
            # Skip tile if it's not water and has already been visited
            if (row, col) in visited:
                return 0
            visited.add((row, col))
            # Get perimeter by searching surrounding tiles for their perimeters
            perimeter = 0
            perimeter += perimeter_dfs(row + 1, col)
            perimeter += perimeter_dfs(row - 1, col)
            perimeter += perimeter_dfs(row, col + 1)
            perimeter += perimeter_dfs(row, col - 1)
            return perimeter
        
        # Search entire grid to find the first land tile to execute perimeter calculation
        for row in range(rows):
            for col in range(cols):
                if grid[row][col] == 1:
                    return perimeter_dfs(row, col)
```
# [472. Concatenated Words](https://leetcode.com/problems/concatenated-words/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
```
# [543. Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def diameterOfBinaryTree(self, root: TreeNode) -> int:
        # max is either (root) 1 + maxleft + maxright, or 1 + max(maxleft, maxright); if node is null, 0
        diameter = 0
        def longest_path(node):
            nonlocal diameter
            if not node:
                return 0
            left_longest = longest_path(node.left)
            right_longest = longest_path(node.right)
            
            # The longest path (diameter) will either be the longest known diameter, or 
            # the longest path of node's left child and right child
            diameter = max(diameter, left_longest + right_longest)
            return max(left_longest, right_longest) + 1
        longest_path(root)
        return diameter
```
# [567. Permutation in String](https://leetcode.com/problems/permutation-in-string/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
```
# [572. Subtree of Another Tree](https://leetcode.com/problems/subtree-of-another-tree/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSubtree(self, s: TreeNode, t: TreeNode) -> bool:
        def validate(s_node, t_node):
            # Base cases: if both node's parents have no children on a given side, return true, or
            # if one node's parent has a child but the other doesn't, it's not matching; return false
            if not s_node and not t_node:
                return True
            if not s_node or not t_node:
                return False
            # If both nodes have the same value (both are equal), check if their children are also equal
            # to determine if the trees are the same
            if s_node.val == t_node.val:
                return (validate(s_node.left, t_node.left) and
                        validate(s_node.right, t_node.right))
        
        # Base cases: if the end of the main tree's subtrees is reached, no matching subtree exists, or
        # if the current subtree is matching, return true (as it's found)
        if not s:
            return False
        if validate(s, t):
            return True
        # Loop case: if the current main tree's subtree isn't matching, check its left and right subtrees
        return self.isSubtree(s.left, t) or self.isSubtree(s.right, t)
```
# [617. Merge Two Binary Trees](https://leetcode.com/problems/merge-two-binary-trees/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def mergeTrees(self, root1: TreeNode, root2: TreeNode) -> TreeNode:
        def sum_nodes(node1, node2):
            if not node1 and not node2:
                return None
            val1 = node1.val if node1 else 0
            val2 = node2.val if node2 else 0
            sum_val = val1 + val2
            left_node = sum_nodes(node1.left if node1 else None, node2.left if node2 else None)
            right_node = sum_nodes(node1.right if node1 else None, node2.right if node2 else None)
            return TreeNode(sum_val, left_node, right_node)
        return sum_nodes(root1, root2)
```
# [637. Average of Levels in Binary Tree](https://leetcode.com/problems/average-of-levels-in-binary-tree/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def averageOfLevels(self, root: TreeNode) -> List[float]:
        averages = []
        queue = collections.deque()
        
        queue.append(root)
        
        # Traverse by levels using BFS; average level = level sum / queue length for that level
        while queue:
            queue_length = len(queue)
            level_sum = 0
            
            for _ in range(queue_length):
                node = queue.popleft()
                if node:
                    level_sum += node.val
                    # Null check before adding children to queue; null values can be added, 
                    # and will mess up the queue length during average calculation
                    if node.left:
                        queue.append(node.left)
                    if node.right:
                        queue.append(node.right)
            averages.append(level_sum / queue_length)
        return averages
```
# [642. Design Search Autocomplete System](https://leetcode.com/problems/design-search-autocomplete-system/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
```
# [654. Maximum Binary Tree](https://leetcode.com/problems/maximum-binary-tree/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
```
# [662. Maximum Width of Binary Tree](https://leetcode.com/problems/maximum-width-of-binary-tree/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
```
# [704. Binary Search](https://leetcode.com/problems/binary-search/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left, right = 0, len(nums) - 1
        while left <= right:
            # Get middle value; calculated like this instead of left + right // 2 due to possible int overflows
            mid = left + (right - left) // 2
            # If the middle value is the target, found value; return it
            if nums[mid] == target:
                return mid
            # If the target is greater than the middle value, search the greater half
            if nums[mid] > target:
                right = mid - 1
            # If not, it must be in the left half, if present
            else:
                left = mid + 1
        # If the value isn't in the array, return -1
        return -1
```
# [720. Longest Word in Dictionary](https://leetcode.com/problems/longest-word-in-dictionary/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
```
# [735. Asteroid Collision](https://leetcode.com/problems/asteroid-collision/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def asteroidCollision(self, asteroids: List[int]) -> List[int]:
        # Track right-moving asteroids with a stack
        asteroid_stack = []
        
        for asteroid in asteroids:
            # There will only be a collision if the current asteroid is moving left (< 0) and 
            # there are asteroids moving right (stored in the stack)
            while asteroid_stack and asteroid < 0 and asteroid_stack[-1] > 0:
                result = asteroid_stack[-1] + asteroid
                # If right-moving was larger, set left-moving to 0 so loop ends and it won't get added to the stack
                if result > 0:
                    asteroid = 0
                # If left-moving was larger, pop from the stack and process next one, if it exists
                elif result < 0:
                    asteroid_stack.pop()
                # If they were the same size, set left-moving to 0 and pop right-moving
                else:
                    asteroid = 0
                    asteroid_stack.pop()
            if asteroid:
                asteroid_stack.append(asteroid)
        return asteroid_stack
```
# [745. Prefix and Suffix Search](https://leetcode.com/problems/prefix-and-suffix-search/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
```
# [828. Count Unique Characters of All Substrings of a Given String](https://leetcode.com/problems/count-unique-characters-of-all-substrings-of-a-given-string/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
```
# [863. All Nodes Distance K in Binary Tree](https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
```
# [876. Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def middleNode(self, head: ListNode) -> ListNode:
        fast, slow = head, head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
        return slow
```
# [904. Fruit Into Baskets](https://leetcode.com/problems/fruit-into-baskets/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def totalFruit(self, tree: List[int]) -> int:
        # max sliding window of at most k distinct elements where k = 2
        left = 0
        baskets = collections.defaultdict(int)
        total_fruit = 0
        for right, tree_type in enumerate(tree):
            baskets[tree_type] += 1
            # If there are more than 2 distinct fruit types, continuously shrink the window
            while len(baskets) > 2:
                baskets[tree[left]] -= 1
                if baskets[tree[left]] == 0:
                    del baskets[tree[left]]
                left += 1
            # The total known amount of fruit possible is either itself, or the size of the current window
            # (since 1 fruit per window index)
            total_fruit = max(total_fruit, right - left + 1)
        return total_fruit
```
# [995. Minimum Number of K Consecutive Bit Flips](https://leetcode.com/problems/minimum-number-of-k-consecutive-bit-flips/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
```
# [1065. Index Pairs of a String](https://leetcode.com/problems/index-pairs-of-a-string/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
```
# [1143. Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        # The DP grid is 1 tile larger than necessary to account for out of bounds cases (out of bounds = 0)
        dp = [[0 for j in range(len(text2) + 1)] for i in range(len(text1) + 1)]
        # Iterate through the grid backwards to b uild up to the main solution
        for i in range(len(text1) - 1, -1, -1):
            for j in range(len(text2) - 1, -1, -1):
                # If both characters are matching, the LCS starting from text1's ith character and
                # text2's jth character is 1 + LCS of the comparison of the next character in both strings 
                if text1[i] == text2[j]:
                    dp[i][j] = 1 + dp[i + 1][j + 1]
                # If not matching, the LCS is the max of either the LCS of the ith character and the j+1th character, or
                # the LCS of the i+1th character and the jth character
                else:
                    dp[i][j] = max(dp[i + 1][j], dp[i][j + 1])
        # Return the result of the first tile
        return dp[0][0]
```
# [1203. Sort Items by Groups Respecting Dependencies](https://leetcode.com/problems/sort-items-by-groups-respecting-dependencies/) 
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
```
# [1299. Replace Elements with Greatest Element on Right Side](https://leetcode.com/problems/replace-elements-with-greatest-element-on-right-side/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def replaceElements(self, arr: List[int]) -> List[int]:
        # Last element should be -1; start with it
        right_max = -1
        # Start at the end, work backwards
        for i in range(len(arr) - 1, -1, -1):
            # Store the rightmost max for the next iteration as either the current max, or the current element
            new_max = max(right_max, arr[i])
            # Set the current element to the rightmost max
            arr[i] = right_max
            # Set the rightmost max to the new max calculated in this iteration
            right_max = new_max
        return arr
```
# [1466. Reorder Routes to Make All Paths Lead to the City Zero](https://leetcode.com/problems/reorder-routes-to-make-all-paths-lead-to-the-city-zero/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
class Solution:
    def minReorder(self, n: int, connections: List[List[int]]) -> int:
        # Store outgoing edge connections in a set to check for changes
        edges = { (a, b) for a, b in connections }
        # Store adjacent node lists in a dict to properly traverse the graph
        neighbors = { city: [] for city in range(n) }
        # Track visited nodes to prevent duplicate visits
        visited = set()
        changes = 0
        
        # Set up neighbor connections using the connections given
        for a, b in connections:
            neighbors[a].append(b)
            neighbors[b].append(a)
            
        def dfs(city):
            nonlocal edges, neighbors, visited, changes
            
            for neighbor in neighbors[city]:
                # If the node has been processed already, skip
                if neighbor in visited:
                    continue
                # If the current neighbor has an edge to the current city,
                # it can reach it, so don't increment changes; otherwise, it needs to be changed
                if (neighbor, city) not in edges:
                    changes += 1
                # Add the current node to visited, and traverse its neighbors
                visited.add(neighbor)
                dfs(neighbor)
        # Start at 0 to get the # of changes for all to reach city 0
        visited.add(0)
        dfs(0)
        return changes
```
