## 一、八皇后问题简介

八皇后问题，是一个古老而著名的问题，是**回溯算法的典型案例**。该问题是国际西洋棋棋手马克斯·贝瑟尔于1848年提出：在8×8格的国际象棋上摆放八个皇后，使其不能互相攻击，即：**任意两个皇后都不能处于同一行、同一列或同一斜线上，问有多少种摆法**。

 ![image-20220109195318551](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220109195325.png)

## 二、八皇后问题算法思路分析（回溯算法）

1)第一个皇后先放第一行第一列

2)第二个皇后放在第二行第一列、然后判断是否OK， 如果不OK，继续放在第二列、第三列、依次把所有列都放完，找到一个合适

3)继续第三个皇后，还是第一列、第二列……直到第8个皇后也能放在一个不冲突的位置，算是找到了一个正确解

4)当得到一个正确解时，在栈回退到上一个栈时，就会开始回溯，即将第一个皇后，放到第一列的所有正确解，全部得到.

5）然后回头继续第一个皇后放第二列，后面继续循环执行 1,2,3,4的步骤 

**说明**：理论上应该创建一个二维数组来表示棋盘，但是实际上可以通过算法，用一个一维数组即可解决问题. arr[8] = {0 , 4, 7, 5, 2, 6, 1, 3} //对应arr 下标 表示第几行，即第几个皇后，arr[i] = val , val 表示第i+1个皇后，放在第i+1行的第val+1列

## 三、代码实现（Java）

```java
package com.fafa.recursion;

/**
 * 八皇后问题，经典的回溯问题
 *
 * @author Sire
 * @version 1.0
 * @date 2022-01-09 14:17
 */
public class EightQueen {
    /**
     * 数组最大容量（也就是皇后数）
     */
    private int max = 8;
    /**
     * 记录列的数组
     */
    private int[] arr = new int[max];
    /**
     * 解法数
     */
    private static int wayCount = 0;
    /**
     * 回溯次数
     */
    private static int recursionCount = 0;

    public static void main(String[] args) {
        EightQueen queen = new EightQueen();
        queen.checkWay(0);
        System.out.println("wayCount = " + wayCount);
        System.out.println("recursion = " + recursionCount);
    }

    /**
     * 检测通路
     */
    public void checkWay(int n) {
        // n == max 也就是也就全部走通过了，因为数组是从0开始的
        if (n == max) {
            showWay();
            return;
        }
        // 给列赋值，同时判断寻路
        for (int i = 0; i < max; i++) {
            // 给列赋值
            arr[n] = i;
            // 如果是通路
            if (judgeWay(n)) {
                // 继续检测下一个
                checkWay(n + 1);
            }
        }
    }

    /**
     * 判断是否为通路
     * 1、两个皇后不能在同一列 (arr[i] == arr[n])、同一行(由于n每次都会累加，所以不用考虑)
     * 2、两个皇后不能在同一斜线上（ 等腰三角形，Math.abs(n - i) == Math.abs(arr[n] - arr[i]) ）
     *
     * @return
     */
    public boolean judgeWay(int n) {
        recursionCount++;
        for (int i = 0; i < n; i++) {
            if (arr[i] == arr[n] || Math.abs(n - i) == Math.abs(arr[n] - arr[i])) {
                return false;
            }
        }
        return true;
    }

    /**
     * 显示通路
     */
    public void showWay() {
        wayCount++;
        for (int i = 0; i < arr.length; i++) {
            System.out.print(arr[i] + "\t");
        }
        // 换行
        System.out.println();
    }
}
```

> ==结果==

如果max = 8的情况下，一共有92中解法，需要回溯15720次

其他皇后结果，只需要该更max值即可

![image-20220109200529853](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220109200530.png)
