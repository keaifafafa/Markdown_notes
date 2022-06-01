## 写在前面

今天再写一个Python小练习的时候，遇到了一个语法错误的问题**TypeError list indices must be integers or slices, not float**

后来仔细分析了下，想起来了了**Python**中的 " / " 与 **Java**和**C语言**里的作用是不一样的，Python里是取到的小数，并非是整数

如果想取整数，需要用 " // "

而且列表里的下标索引是不允许为小数的，故出现了如上的语法问题

## 练习代码

```python
"""
计算数集中的中位数
实训思路及步骤
(1) sorted函数可对列表中的元素进行排序。
(2）使用下标可获取列表中对应位置的元素。
(3）列表中元素的个数为奇数时，中位数为列表正中间位置的那个数。
(4) 列表中元素的个数为偶数时，中位数为列表正中间位置的两个数的均值。
"""


# 获取中位数
def get_mid_num(*nums):
    # 先排序(这种不会改变原列表)
    new_nums = sorted(nums)
    # 计算其长度
    n = len(new_nums)
    # 如果长度为奇数,直接去取中间数即可
    if n % 2 != 0:
        # 需要注意list下标索引不能为float类型，所以需要使用 " // "
        return new_nums[n // 2]
    # 如果为偶数,取中间两数的均值
    else:
        return (new_nums[n // 2] + new_nums[n // 2 - 1]) / 2

# 调用函数获取中位数
print(get_mid_num(2, 3, 5, 1, 6, 7))

```

