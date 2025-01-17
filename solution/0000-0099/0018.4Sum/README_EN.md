# [18. 4Sum](https://leetcode.com/problems/4sum)

[中文文档](/solution/0000-0099/0018.4Sum/README.md)

## Description

<p>Given an array <code>nums</code> of <code>n</code> integers, return <em>an array of all the <strong>unique</strong> quadruplets</em> <code>[nums[a], nums[b], nums[c], nums[d]]</code> such that:</p>

<ul>
	<li><code>0 &lt;= a, b, c, d&nbsp;&lt; n</code></li>
	<li><code>a</code>, <code>b</code>, <code>c</code>, and <code>d</code> are <strong>distinct</strong>.</li>
	<li><code>nums[a] + nums[b] + nums[c] + nums[d] == target</code></li>
</ul>

<p>You may return the answer in <strong>any order</strong>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [1,0,-1,0,-2,2], target = 0
<strong>Output:</strong> [[-2,-1,1,2],[-2,0,0,2],[-1,0,0,1]]
</pre>

<p><strong>Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [2,2,2,2,2], target = 8
<strong>Output:</strong> [[2,2,2,2]]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 200</code></li>
	<li><code>-10<sup>9</sup> &lt;= nums[i] &lt;= 10<sup>9</sup></code></li>
	<li><code>-10<sup>9</sup> &lt;= target &lt;= 10<sup>9</sup></code></li>
</ul>


## Solutions

<!-- tabs:start -->

### **Python3**

```python
class Solution:
    def fourSum(self, nums: List[int], target: int) -> List[List[int]]:
        res = []
        if nums is None or len(nums) < 4:
            return res
        n = len(nums)
        nums.sort()
        for i in range(n - 3):
            if i > 0 and nums[i] == nums[i - 1]:
                continue
            for j in range(i + 1, n - 2):
                if j > i + 1 and nums[j] == nums[j - 1]:
                    continue
                p, q = j + 1, n - 1
                while p < q:
                    if p > j + 1 and nums[p] == nums[p - 1]:
                        p += 1
                        continue
                    if q < n - 1 and nums[q] == nums[q + 1]:
                        q -= 1
                        continue
                    t = nums[i] + nums[j] + nums[p] + nums[q]
                    if t == target:
                        res.append([nums[i], nums[j], nums[p], nums[q]])
                        p += 1
                        q -= 1
                    elif t < target:
                        p += 1
                    else:
                        q -= 1
        return res
```

### **Java**

```java
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        int n;
        if (nums == null || (n = (nums.length)) < 4) {
            return Collections.emptyList();
        }
        Arrays.sort(nums);
        List<List<Integer>> res = new ArrayList<>();
        for (int i = 0; i < n - 3; ++i) {
            if (i > 0 && nums[i] == nums[i - 1]) {
                continue;
            }
            for (int j = i + 1; j < n - 2; ++j) {
                if (j > i + 1 && nums[j] == nums[j - 1]) {
                    continue;
                }
                int p = j + 1, q = n - 1;
                while (p < q) {
                    if (p > j + 1 && nums[p] == nums[p - 1]) {
                        ++p;
                        continue;
                    }
                    if (q < n - 1 && nums[q] == nums[q + 1]) {
                        --q;
                        continue;
                    }
                    int t = nums[i] + nums[j] + nums[p] + nums[q];
                    if (t == target) {
                        res.add(Arrays.asList(nums[i], nums[j], nums[p], nums[q]));
                        ++p;
                        --q;
                    } else if (t < target) {
                        ++p;
                    } else {
                        --q;
                    }
                }
            }
        }
        return res;
    }
}
```
### **JavaScript**
```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[][]}
 */
var fourSum = function (nums, target) {
    let len = nums.length;
    let res = [];
    if (len < 4) return [];
    nums.sort((a, b) => a - b);
    for (i = 0; i < len - 3; i++) {
        if (i > 0 && nums[i] === nums[i - 1]) continue;
        if (nums[i] + nums[len - 1] + nums[len - 2] + nums[len - 3] < target) continue;
        if (nums[i] + nums[i + 1] + nums[i + 2] + nums[i + 3] > target) break;
        for (j = i + 1; j < len - 2; j++) {
            if (j > i + 1 && nums[j] === nums[j - 1]) continue;
            let left = j + 1, right = len - 1;
            while (left < right) {
                if (nums[i] + nums[j] + nums[left] + nums[right] === target) {
                    res.push([nums[i], nums[j], nums[left], nums[right]]);
                    while (nums[left] === nums[left + 1]) left++;
                    left++;
                    while (nums[right] === nums[right - 1]) right--;
                    right--;
                    continue;
                } else if (nums[i] + nums[j] + nums[left] + nums[right] > target) {
                    right--;
                    continue;
                } else {
                    left++;
                    continue;
                }
            }
        }
    }
    return res;
};
```

### **...**

```

```

<!-- tabs:end -->
