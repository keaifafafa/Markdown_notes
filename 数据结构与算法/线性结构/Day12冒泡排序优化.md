## 前言：

冒泡排序是很稳定且简单的一种排序，适合小数排序，这里主要讲解冒泡排序如何进行优化

## 实现思路及代码

> ==优化思路==

- 有时，我们进行排序时，有可能已经完全排好了，但是循环还没有停，因为并没有循环遍历结束，所以还在继续浪费时间，进行遍历

- 这时候，我们可以设置一个哨兵（flag），如果一次遍历下来没有发生数字置换，那么就可以证明，顺序已经排好，无需再进行下一次循环遍历了

- 然后，哨兵（flag）的状态也发生改变，最后在第二层循环结束时，进行判断哨兵（flag）的状态进行相应的操作即可。

> ==代码实现==

```java
/**
     * 冒泡排序
     *
     * @param arr
     */
public static void sort(int[] arr) {
    // 循环的次数
    int count = 0;
    // 标识变量，标识是否进行过交换
    boolean flag = false;
    int temp = 0;
    for (int i = 0; i < arr.length - 1; i++) {
        for (int j = i; j < arr.length; j++) {
            if (arr[i] > arr[j]) {
                flag = true;
                temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
            count++;
        }
        // 直接停止
        if (!flag) {
            break;
        } else {
            flag = false;
        }
    }
    // 打印遍历的次数
    System.out.println("循环遍历了" + count);
}
```

