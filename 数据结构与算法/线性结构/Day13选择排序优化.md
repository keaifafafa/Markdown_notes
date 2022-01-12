

## 选择排序简介

选择式排序也属于内部排序法，是从欲排序的数据中，按指定的规则选出某一元素，再依规定交换位置后达到排序的目的。

## 选择排序思路分析图

 ![image-20220112211432324](https://gitee.com/lovely-hair/blog-img/raw/master/img/20220112211440.png)

## 如何优化选择排序

> ==思路==

建议在一定数据量的情况下查看效果，比如排序80000个随机数据，会比未优化的快很多（效果很明显）

因为减少了很多没必要的置换，未优化前的选择，其实和冒泡很相似（只不过冒泡是先把后面的排好，选择是先把前面的排好）

```java
选择排序（已优化）
* 思路:
* 1、首先，先假定最小值和最小值的下标索引
* 2、然后进行寻找，如果找到比最小值还要小的，进行最小值和最小值下表索引的重置
* 3、然后进行位置置换（换到本次循环的头元素位置，即 i ）
```

> ==实现代码==

```java
/**
     * 选择排序（已优化）
     * 思路:
     * 1、首先，先假定最小值和最小值的下标索引
     * 2、然后进行寻找，如果找到比最小值还要小的，进行最小值和最小值下表索引的重置
     * 3、然后进行位置置换（换到本次循环的头元素位置，即 i ）
     * @param nums
     */
public static void selectSort(int[] nums){
    for(int i = 0; i < nums.length - 1; i++){
        int min = nums[i];
        int minIndex = i;
        for (int j = i + 1; j < nums.length; j++){
            // 如果最小值 比 后面的数大
            if (min > nums[j]){
                // 给最小值和最小值的下标 赋值（更小的值）
                min = nums[j];
                // 重置 minIndex
                minIndex = j;
            }
        }
        // 置换位置(这样可以减少不必要的置换,比如本身就在目标位置的情况下)
        if (minIndex != i){
            nums[minIndex] = nums[i];
            nums[i] = min;
        }
    }
}
```

> ==未优化的代码==

```java
/**
     * 未优化的选择排序
     * @param nums
     */
public static void selectSort2(int[] nums){
    int temp = 0;
    for (int i= 0; i < nums.length - 1; i++){
        for (int j = i + 1; j < nums.length; j++){
            // 说明假设的最小值，并非最小值
            if (nums[i] > nums[j]){
                temp = nums[i];
                nums[i] = nums[j];
                nums[j] = temp;
            }
        }
    }
}
```

