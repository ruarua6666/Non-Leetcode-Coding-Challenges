# pdd常见代码题

## 最长先递增再递减的序列

### 题目描述

找到一个数组里最长的先递增再递减序列。

### 解决方案

找到每个最高点，然后遍历每个最高点，求结果。

### 代码

```python
nums = [1, 2, 3, 1]

targets = []

# 在 nums 的开头和结尾各添加一个 0
nums = [0] + nums + [0]  # nums 变为 [0, 1, 2, 3, 1, 0]

# 寻找峰值的索引（比相邻元素都大）
for i in range(1, len(nums)-1):
    if nums[i] > nums[i+1] and nums[i] > nums[i-1]:
        targets.append(i)

res = 0

# 去掉开头和结尾添加的 0，恢复原始的 nums
nums = nums[1:len(nums)-1]  # nums 变为 [1, 2, 3, 1]

for target in targets:
    target = target - 1  # 索引调整，因为开头加了pivot
    left, right = target - 1, target + 1

    # 向左扩展，找到左边界
    while left >= 0 and nums[left] < nums[left+1]:
        left -= 1

    # 向右扩展，找到右边界
    while right < len(nums) and nums[right] < nums[right-1]:
        right += 1

    # 更新结果
    res = max(res, right - left + 1)

print(res)
```