---
// title: "firstPost"
date: "2024-05-02T23:59:48+08:00"
draft: false
---

## My Golang Leetcode Journey which starts from Binary Search. (1)

![People coding](/img/peopleCoding.jpg)

I started with Binary Search and separated them into groups based on Huahua’s list on [his website](https://zxi.mytechroad.com/blog/leetcode-problem-categories/).
Rotated is the first topic I practice, and I hope that putting my record here will push me to 1. write more code, 2. think deeper, 3. remember to go through it again before interviewing without not knowing where my notes are, and also 4. make connections with people.
### 1. Search for a specific target in rotated, sorted arrays

#### [33. Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) (To do: find the target)
    Template in pseudocode:
    // pseudocode
    // determine where the pivot is
        nums[mid] == target
        nums[mid] > nums[l] // the pivot is on the right hallf
            // determine the relationship between target, nums[l] and nums[mid] 
        nums[mid] < nums[l] // the pivot is on the left half
            // determine the relationship between target, nums[r] and nums[mid]

</code></pre>

    func search(nums []int, target int) int {
        l, r := 0, len(nums) - 1
        for l <= r {
            mid := (l + r) / 2
            if nums[mid] == target {
                return mid
            } else if nums[mid] >= nums[l] {
                if nums[l] <= target && target < nums[mid] {
                    r = mid - 1
                } else {
                    l = mid + 1
                }
            } else { // nums[mid] < nums[l]
                if nums[mid] < target && target <= nums[r] {
                    l = mid + 1
                } else {
                    r = mid - 1
                } 
            }
        }
        return -1
    }

#### [81. Search in Rotated Sorted Array II](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/) (To do: find the target as question 33, but this one’s different since the values of nums is NOT UNIQUE)
    Template in pseudocode:
    // pseudocode
    // remember to use a while loop to determine whether a number is duplicate
    // if so, ignore it
    for l <= r {
            for l < r && nums[l] == nums[l+1] {
                l++
            }
            for l < r && nums[r] == nums[r-1] {
                r--
            }
    // others are the same as the former question

</code></pre>

    func search(nums []int, target int) bool {
        l, r := 0, len(nums) - 1
        for l <= r {
            for l < r && nums[l] == nums[l+1] {
                l++
            }
            for l < r && nums[r] == nums[r-1] {
                r--
            }
            mid := (l + r) / 2
            if nums[mid] == target {
                return true
            }
            if nums[mid] >= nums[l] {
                if nums[l] <= target && target < nums[mid] {
                    r = mid - 1
                } else {
                    l = mid + 1
                }
            } else if nums[mid] < nums[l] {
                if nums[mid] < target && target <= nums[r] {
                    l = mid + 1
                } else {
                    r = mid - 1
                }
            } 
        } 
        return false
    }
### 2. Search for the minimum is rotated, sorted arrays

### 3. Search for the peak