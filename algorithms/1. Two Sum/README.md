# 1. Two Sum

<details>
  <summary>Problem statement</summary>

<pre>
Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.
You can return the answer in any order.

Example 1:
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].

Example 2:
Input: nums = [3,2,4], target = 6
Output: [1,2]

Example 3:
Input: nums = [3,3], target = 6
Output: [0,1]
 

Constraints:
2 <= nums.length <= 104
-109 <= nums[i] <= 109
-109 <= target <= 109
Only one valid answer exists.
 

Follow-up: Can you come up with an algorithm that is less than O(n2) time complexity?
</pre>

</details>

**Brute Force Approach**  <br>
* This approach involves iterating through all possible pairs of numbers to find the two that sum up to the target value. While straightforward, it is inefficient for large inputs due to its quadratic time complexity.
* Time Complexity :  $O(n^2)$
* Space Complexity : $O(1)$ 

  
```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int n = (int)nums.size();
        for(int i=0; i < n; i++){
            for(int j = i + 1; j < n; j++){
                if( nums[i] + nums [j] == target ){
                    return {i, j};
                }
            }
        }
        return {};
    }
};
```

**Hash Map Approach** <br>
* By using a hash map (or unordered map), we can achieve a linear time complexity solution. This approach involves storing each number and its index in the hash map as we iterate through the array. For each number, we check if the complement (i.e., target - number) exists in the hash map. This method provides a significant efficiency improvement over the brute force approach.

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> mp; // Hash map to store number and its index
        iint n = (int)nums.size(); // Get the size of the vector

        for (int i = 0; i < n; i++) {
            int complement = target - nums[i]; // Calculate the complement
            // Check if the complement exists in the hash map
            if (mp.find(complement) != mp.end()) {
                return { mp[complement], i }; // Return indices if found
            }
            // Store the number and its index in the hash map
            mp[nums[i]] = i;
        }
        // Return an empty vector if no solution is found
        return {};
    }
};
```