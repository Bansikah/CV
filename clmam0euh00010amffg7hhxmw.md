---
title: "Binary Search in Python"
datePublished: Fri Sep 08 2023 13:04:49 GMT+0000 (Coordinated Universal Time)
cuid: clmam0euh00010amffg7hhxmw
slug: binary-search-in-python
tags: algorithms, python, binary-search-algorithm, pythonprogrammi

---

# Intuition

Binary search is an efficient array search algorithm. It works by narrowing down the search range by half each time. If you have looked up a word in a physical dictionary, you've already used binary search in real life. Let's look at a simple example:

Given a sorted array of integers and an integer called <mark>target</mark>, find the element that equals the target and return its index. If the element is not found, return `-1`.

The key observation here is that the array is sorted. We pick a random element in the array and compare it to the target.

\-&gt; If we happen to pick the element that equals the target (how lucky!), then bingo. We don't need to do any more work; return its index.

\-&gt; If the element is smaller than the target, then we know the target cannot be found in the section to the left of the current element since everything to the left is even smaller. So we discard the current element and everything on the left from the search range.

\-&gt; If the element is larger than the target, then we know the target cannot be found in the section to the right of the current element since everything to the right is even larger. So we discard the current element and everything on the right from the search range. We repeat this process until we find the target. Instead of picking a random element, we always pick the middle element in the current search range.

This way, we can discard half of the options and shrink the search range by half each time. This gives us `O(log(N))` runtime.

This idea can be implemented both iteratively and recursively. However, the major difference is that the iterative version of binary search uses `O(1)` memory while the recursive version uses `O(log(N))` memory.

## Implementation

The search range is represented by the `left` and `right` indices that start from both ends of the array and move towards each other as we search. When moving the index, we discard elements and shrink the search range.

Time Complexity: `O(log(n))`

```python
from typing import List

def binary_search(arr: List[int], target: int) -> int:
    left, right = 0, len(arr) - 1
    while left <= right:  # <= because left and right could point to the same element, < would miss it
        mid = (left + right) // 2 # double slash for integer division in python 3, we don't have to worry about integer `left + right` overflow since python integers can be arbitrarily large
        # found target, return its index
        if arr[mid] == target:
            return mid
        # middle less than target, discard left half by making left search boundary `mid + 1`
        if arr[mid] < target:
            left = mid + 1
        # middle greater than target, discard right half by making right search boundary `mid - 1`
        else:
            right = mid - 1
    return -1 # if we get here we didn't hit above return so we didn't find target

if _name_ == '_main_':
    arr = [int(x) for x in input().split()]
    target = int(input())
    res = binary_search(arr, target)
    print(res)
```

Calculatating `mid`

Note that when calculating `mid`, if the number if elements is even, there are two elements in the middle. We usaully follow the convention of picking the first one, equivalent to doing integer division `(left + right) / 2.`

In most programming languages, we calculate mid with `left + floor((right-left) / 2)` to avoid potential integer overflow. However, in Python, we do not need to worry about `left + right` integer overflow because Python3 integers can be arbitrarily large.

## Deducing binary search

It's essential to understand and deduce the algorithm yourself instead of memorizing it. In an actual interview, interviewers may ask you additional questions to test your understanding, so simply memorizing the algorithm may not be enough to convince the interviewer.

Key elements in writing a correct binary search:

1. ### When to terminate the loop
    
    Make sure the `while` loop has an equality comparison. Otherwise, we'd skip the loop and miss the potential match for the edge case of a one-element array.
    
2. ### Whether/how to update `left` and `righ`t boundary in the `if` conditions
    
    Consider which side to discard. If `arr[mid]` is already smaller than the `target`, we should discard everything on the left by making `left = mid + 1.`
    
3. ### Should I discard the current element?
    
    For vanilla binary search, we can discard it since it can't be the final answer if it is not equal to the target. There might be situations where you would want to think twice before discarding the current element. We'll discuss this in the next module.
    

## When to use Binary Search

Binary search is particularly useful when you have a large sorted dataset and you need to quickly locate a specific element. Its time complexity is O(log n), where n is the size of the dataset. This makes it significantly faster than linear search, which has a time complexity of O(n).

Here are a few situations where binary search can be applied:

1. Searching in a sorted list: If you have a sorted list or array and need to find a specific value, binary search is an excellent choice. Since the list is sorted, binary search can quickly narrow down the search space by comparing the target value with the middle element and then recursively performing the search on the appropriate half of the list.
    
2. Finding boundaries or insertion points: Binary search can also be used to find the lower and upper boundaries of a value in a sorted list. This can be useful when you want to know the range of elements equal to a target value or determine the correct position to insert an element while maintaining the sorted order.
    
3. Efficiently solving optimization problems: Binary search can be an integral part of certain optimization problems. For example, consider a problem where you need to find the maximum or minimum value that satisfies a given condition in a sorted list. Binary search can help you efficiently narrow down the range of values to search and converge on the optimal solution.
    

It is worth mentioning that binary search has some prerequisites. The list or array must be sorted, and random access to elements is required. This means that binary search is not suitable for linked lists or other data structures where accessing arbitrary elements is not efficient.

I hope this clarifies when to use binary search! If you have any further questions, feel free to ask and also contribute better approach that could be used. Adios