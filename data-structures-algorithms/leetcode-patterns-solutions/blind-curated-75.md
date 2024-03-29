# Overview
Problems, solutions, and solutiton code are taken from LeetCode solutions. Links to the problems on LeetCode are included with each question.
# []()
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
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
# [33. Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
# TODO: Logic not understood fully still; return to this
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left, right = 0, len(nums) - 1
        while left <= right:
            # Integer division to get the middle of the array
            mid = (left + right) // 2
            # If the middle is the target, return it
            if nums[mid] == target:
                return mid
            # Use knowledge of a sorted array to determine if mid is in the bigger or smaller portion of the array;
            # in a sorted array, every element should be <= the leftmost element.
            # If mid is in the lesser half, ...
            if nums[left] <= nums[mid]:
                if target > nums[mid] or target < nums[left]:
                    left = mid + 1
                else:
                    right = mid - 1
            # If mid is in the greater half, ...
            else:
                if target < nums[mid] or target > nums[right]:
                    right = mid - 1
                else:
                    left = mid + 1
        return -1
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
# [98. Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)
## Information
## Question
## Solutions
## Notes
## Solution Code
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
# 3. Longest Substring Without Repeating Characters
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
# 5. Longest Palindromic Substring
# 128. Longest Consecutive Sequence
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
# 11. Container With Most Water
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
# 15. 3Sum
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
# [295. Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/)
## Information
## Question
## Solutions
## Notes
## Solution Code
``` py
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
# 20. Valid Parentheses
* stack? check answer again
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
# 23. Merge k Sorted Lists
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
# [146. LRU Cache](https://leetcode.com/problems/lru-cache/)
ordered dict (java: linkedhashtable)?
# [91. Decode Ways](https://leetcode.com/problems/decode-ways/)
* decision tree w/ memoization (recursion); keep track of this until you fully understand recursion/dp (topdown/bottomup)